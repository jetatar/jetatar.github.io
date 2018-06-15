# Troubleshooting a Slurm partition in a 'DOWN' state

## Processes

### On Master
```
[root@xcat2-master ~]# ps aux | grep slurm
slurm     1439  0.0  0.1 668460  5904 ?        Sl   Jun14   0:23 /usr/sbin/slurmctld
slurm     1926  0.0  0.0 276508  2456 ?        Sl   Jun14   0:00 /usr/sbin/slurmdbd
```

### On Compute

## Log files
### On Master
/var/log/slurmctrld.log
/var/log/slurmsched.log
/var/log/slurm/slurmdbd.log

### On Compute
/var/log/slurmd.log

## Running Daemons

### On Master Slurm Server:

Make sure the following daemons are running:
_slurmctrld, slurmdbd, munged_

### On Compute Node Slurm Instance:
_slurmd, munged_
