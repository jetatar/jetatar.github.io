# Configuring an Elastic Cloud Partition

## References
_https://slurm.schedmd.com/power_save.html_
_http://biocluster.ucr.edu/~jhayes/slurm/elastic_computing.html_


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
### On Compute
Make sure the following daemons are running:
_slurmd, munged_
```
[root@nfs-1 ~]# ps aux | grep slurm
root     20214  0.0  0.1 131304  2552 ?        S    Jun13   0:00 /usr/sbin/slurmd
[root@nfs-1 ~]# ps aux | grep munged
munge      970  0.0  0.1 243956  2464 ?        Sl   May08   0:15 /usr/sbin/munged
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
