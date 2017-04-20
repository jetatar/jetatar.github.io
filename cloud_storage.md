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
   Storage> 7
```

   Q4:<br>
   ```
   Google Application Client Id - leave blank normally.
   client_id>
   ```
   
   Q5:<br>
   ```
   Google Application Client Secret - leave blank normally.
   client_secret>
   ```
   Q6:<br>
   ```
   Use auto config?
   * Say Y if not sure
   * Say N if you are working on a remote or headless machine or Y didn't work
   y) Yes
   n) No
   y/n> n
   ```
   If a browser doesn't automatically show up and ask you to login using your UCI account, use your favorite browser and enter go to the link that was generated and enter the verification code that is printed after you allow RClone to use your Google Drive account:
   ```
   If your browser doesn't open automatically go to the following link: https://accounts.google.com/o/oauth2/authclient_id=202264815644.apps.googleusercontent.com&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive&state=3203235a96b6c69143da28d4570c4df4
Log in and authorize rclone for access
Enter verification code> 4/5qfmM5b2B1vgRzCeXUGdYNrMgRvrfF6ycTv2fpiaCME
   ```
   After entering the verification code, you will see the rclone.config file configuration entry in $HOME/.config/rclone/: 
   ```
   --------------------
   [gDrive]
   client_id =
   client_secret =
   token = {"access_token":"ya29.GlsyBNeHGVXOwiKz4f5qu9R-IVVV7mgalSGVTK0v_snzHuKU3YpAs3D0An
  KLbR5pkl_jqHqrNSA5l4regTfgHl7GWe7vpj5SPGLnKOvp_eEQ24GgrZdbSb9Flks","token_type":"Bearer","refresh_token":"1/_X4omasTIoXnO4k9SGcmri-S4XDTsBxA2MzxgrrxmYTU0nJZ3Os_N3lqzhyUqZo","expiry":"2017-04-19T16:15:32.557926381-07:00"}
  --------------------
  y) Yes this is OK
  e) Edit this remote
  d) Delete this remote
  y/e/d> y
   ```

Current remotes:

Name                 Type
====                 ====
gDrive               drive

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q   
   
### Backup to Cloud from HPC

### Retreiving Backup from Cloud to HPC

### Archival Storage
