# Troubleshooting a Slurm partition in a 'DOWN' state

## On Master Slurm Server:

Make sure the following daemons are running:
slurmctrld, slurmdbd, munged

## On Compute Node Slurm Instance:
slurmd, munged
