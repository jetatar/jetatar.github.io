### UCI HPC Cloud Data Storage and Backup

HPC users at UCI can use an open source app named [`rclone`](https://rclone.org/) to **manually** transfer data between HPC and a number of `rclone` supported cloud data storage providers (i.e: Google Drive, Amazon S3, Dropbox etc).  

### RClone Configuration
1. Login to the interactive node on HPC

   From your personal computer ssh to HPC:<BR>
   `ssh -X -Y yourusername@hpc.oit.uci.edu`

   From the HPC login node connect to the interactive node:<BR>
   `ssh -X -Y compute-1-13`

2. Load the RClone module:

   `module load rclone`

3. To Configure RClone interactively run:

   `rclone config`
   
   Answer the questions:
   Q1:
   
   ``No remotes found - make a new one
      n) New remote
      s) Set configuration password
      q) Quit config``

### Backup to Cloud from HPC

### Retreiving Backup from Cloud to HPC

### Archival Storage
