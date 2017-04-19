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
   
   Q1:<br>
   ```
   No remotes found - make a new one
      n) New remote
      s) Set configuration password
      q) Quit config
   n/s/q> n
   name> gDrive
   ```
   
   Q2:<br>
   
   ```
   Type of storage to configure.
   Choose a number from below, or type in your own value
    1 / Amazon Drive
      \ "amazon cloud drive"
    2 / Amazon S3 (also Dreamhost, Ceph, Minio)
      \ "s3"
    3 / Backblaze B2
      \ "b2"
    4 / Dropbox
      \ "dropbox"
    5 / Encrypt/Decrypt a remote
      \ "crypt"
    6 / Google Cloud Storage (this is not Google Drive)
      \ "google cloud storage"
    7 / Google Drive
      \ "drive"
    8 / Hubic
      \ "hubic"
    9 / Local Disk
      \ "local"
   10 / Microsoft OneDrive
      \ "onedrive"
   11 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
      \ "swift"
   12 / Yandex Disk
      \ "yandex"
   Storage>
```
   
   
   
### Backup to Cloud from HPC

### Retreiving Backup from Cloud to HPC

### Archival Storage
