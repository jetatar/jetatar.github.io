### UCI HPC Cloud Data Storage and Backup

HPC users at UCI can use an open source app named [`rclone`](https://rclone.org/) to **manually** transfer data between HPC and a number of `rclone` supported cloud data storage providers (i.e: Google Drive, Amazon S3, Dropbox etc).  

### RClone Configuration
1. Login to the interactive node on HPC:
  `ssh -X username@hpc.oit.uci.edu`
  `qrsh`

2. Load the RClone module:

   `module load rclone`

3. To Configure RClone run:

   `rclone config`

### Backup to Cloud from HPC

### Retreiving Backup from Cloud to HPC

### Archival Storage
