# Troubleshooting a Slurm partition in a 'DOWN' state

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
