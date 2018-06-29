# Configuring an Elastic Cloud Partition
Slurm's ability to extend into the could relies on its Power Save capabilities.  The Slurm Power Save module provides for a way to regulate nodes or queues' states based on usage or some other partition attribute.  With execution of pre- and post- scripting allowed by Power Save, nodes can be assimilated from AWS (and others) and disbanded when the cloud nodes are no longer needed.  To be able to do that successfully, Slurm needs to ultimately have a way of getting the AWS cloud nodes' names and IP addresses, unless the AWS instance is assigned a static IP and hostname.

## Setup

* Setup Global Users
* Install, setup, and enable MariaDB
* Install, setup and enable Munge
* Install, setup and enable Slurm


### Global Users (all nodes, setup before Slurm or Munge install)

Slurm and Munge require UID and GID to be the same across all nodes.







### MariaDB (master slurm instance, install before Slurm)
Slurm can store various accounting data in MariaDB.  It only needs to bet setup on the node that will run the master slurm instance.

If not installed, install MariaDB:

```yum install mariadb-server mariadb-devel -y```


### Munge (all nodes, install before Slurm)

Munge is an authentication tool used to identify messaging from the Slurm machines.
Install munge on all nodes:
```
yum install epel-release
yum install munge munge-libs munge-devel -y
```
After installing Munge, create a secret key **only on the slurm server node**, where munge will also be running by:
```
yum install rng-tools -y
rngd -r /dev/urandom
/usr/sbin/create-munge-key -r 
dd if=/dev/urandom bs=1 count=1024 > /etc/munge/munge.key
chown munge: /etc/munge/munge.key
chmod 400 /etc/munge/munge.key
```
At the end it should look something like this:
```
[root@xcat2-master ~]# ls -la /etc/munge/munge.key
-r-------- 1 munge munge 1024 Feb  1 12:35 /etc/munge/munge.key
```
This key should now be propagated to all of the compute nodes in the cluster:
```
scp /etc/munge/munge.key root@nfs-1:/etc/munge
scp /etc/munge/munge.key centos@18.237.111.190:/etc/munge (ie: cloud instance)
```
Then login to every node, correct permissions and start the munge daemon:
```
chown -R munge: /etc/munge/ /var/log/munge/
chmod 0700 /etc/munge/ /var/log/munge/
systemctl enable munge
systemctl start munge
```
Test communication between Munge clients.  From the slurm master node try:
```
munge -n
munge -n | unmunge
munge -n | ssh nfs-1 unmunge
remunge
```
If no errors are encoutered, Munge is working as expected.

## SLURM

Create Slurm RPMS to install on all nodes:
```
rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
yum install -y munge-devel munge-libs readline-devel perl-ExtUtils-MakeMaker openssl-devel pam-devel rpm-build perl-DBI perl-Switch munge mariadb-devel
```
Download the desired version of Slurm from: https://www.schedmd.com/downloads.php
Then build the RPM packages:

```
rpmbuild -ta slurm-17.11.2.tar.bz2
```
Now install the RPMs **on all nodes**:
```
rpm -Uvh ~/rpmbuild/RPMS/x86_64/*.rpm
```

### Create and Configure slurm.conf

On the master slurm node, create a slurm.conf file, as the one [https://github.com/jetatar/Docs/blob/master/slurm.conf](here).



**SelectType**

Generally must be "select/linear". If Slurm is configured to allocate individual CPUs to jobs rather than whole nodes (e.g. SelectType=select/cons_res rather than SelectType=select/linear), then Slurm maintains bitmaps to track the state of every CPU in the system. If the number of CPUs to be allocated on each node is not known when the slurmctld daemon is started, one must allocate whole nodes to jobs rather than individual processors. The use of "select/cons_res" requires each node to have a CPU count set and the node eventually selected must have at least that number of CPUs.

## References
_https://slurm.schedmd.com/power_save.html_

_http://biocluster.ucr.edu/~jhayes/slurm/elastic_computing.html_

_https://slurm.schedmd.com/quickstart_admin.html_

_http://sysadm.mielnet.pl/building-and-installing-rpm-slurm-on-centos-7/_


# Troubleshooting a Slurm Partition in a 'DOWN' State
## Check Node Status
```
[root@xcat2-master ~]# sinfo
PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
testQ*       up   infinite      1   down nfs-1
```
If the state is _down_, ping the machine(s) and see if they respond:
`ping nfs-1`

## Check Daemons
### On Master
Make sure the following daemons are running:
_slurmctrld, slurmdbd, munged_
```
[root@xcat2-master ~]# ps aux | grep slurm
slurm     1439  0.0  0.1 668460  5904 ?        Sl   Jun14   0:23 /usr/sbin/slurmctld
slurm     1926  0.0  0.0 276508  2456 ?        Sl   Jun14   0:00 /usr/sbin/slurmdbd
[root@xcat2-master ~]# ps aux | grep munged
munge     1092  0.0  0.0 243956  2216 ?        Sl   Jun14   0:00 /usr/sbin/munged
```
Check munge:
```
munge -n | unmunge | grep STATUS
STATUS:           Success (0)
```

### On Compute
Make sure the following daemons are running:
_slurmd, munged_
```
[root@nfs-1 ~]# ps aux | grep slurm
root     20214  0.0  0.1 131304  2552 ?        S    Jun13   0:00 /usr/sbin/slurmd
[root@nfs-1 ~]# ps aux | grep munged
munge      970  0.0  0.1 243956  2464 ?        Sl   May08   0:15 /usr/sbin/munged
```
Check munge:
```
munge -n | unmunge | grep STATUS
STATUS:           Success (0)
```

## Check the Logs
### On Master
/var/log/slurmctrld.log
/var/log/slurmsched.log
/var/log/slurm/slurmdbd.log
/var/log/munge/*
### On Compute
/var/log/slurmd.log
/var/log/munge/*

## Restart Daemons (Master first)
First restart the master node's _slurmctrld_ process:
_sudo systemctl restart slurmctrld_
If issues persist, restart _slurmd_ on compute node next:
_sudo systemctl restart slurmd_

## Able to ssh from master to compute node?
You should be able to ssh from master to compute node without having to enter a password.  If that is not the case, create a ssh key and copy the public key to the compute node.

Then, try, in this order:
Stop the _slurmd_ instance on the compute node.
Restart the _slurmctrld_ instance on the master node.
Start the _slurmd_ instance on the compute node.

## Last resort 
_scontrol update nodename=nfs-1 state=resume_

## References:
_https://www.eidos.ic.i.u-tokyo.ac.jp/~tau/lecture/parallel_distributed/2016/html/fix_broken_slurm.html_
_https://slurm.schedmd.com/troubleshoot.html_
