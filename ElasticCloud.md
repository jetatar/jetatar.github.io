# Troubleshooting a Slurm partition in a 'DOWN' state

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
```
[root@xcat2-master ~]# ps aux | grep slurm
slurm     1439  0.0  0.1 668460  5904 ?        Sl   Jun14   0:23 /usr/sbin/slurmctld
slurm     1926  0.0  0.0 276508  2456 ?        Sl   Jun14   0:00 /usr/sbin/slurmdbd
[root@xcat2-master ~]# ps aux | grep munged
munge     1092  0.0  0.0 243956  2216 ?        Sl   Jun14   0:00 /usr/sbin/munged
```
### On Compute
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

## Running Daemons
Make sure the following daemons are running:
_slurmctrld, slurmdbd, munged_
### On Compute Node Slurm Instance:
_slurmd, munged_
