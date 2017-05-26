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

   Q7: If a browser doesn't automatically show up and ask you to login using your UCI account, use your favorite browser and enter go to the link that was generated and enter the verification code that is printed after you allow RClone to use your Google Drive account:<br>
   ```
   If your browser doesn't open automatically go to the following link:
      https://accounts.google.com/o/oauth2/authclient_id=202264815644.apps.googleusercontent.com&redirect_uri=urn%3Aietf%3Awg%3Aoauth%3A2.0%3Aoob&response_type=code&scope=https%3A%2F%2Fwww.googleapis.com%2Fauth%2Fdrive&state=250febf5c0532c7209789b54e032d2e5
   
   Log in and authorize rclone for access
   Enter verification code> 4/5qfmM5b2B1vgRzCeXUGdYNrMgRvrfF6ycTv2fpiaCME
   ```
   Q8: After entering the verification code, you will see the rclone.config file configuration entry in $HOME/.config/rclone/:<br>
   ```
   --------------------
   [gDrive]
   client_id =
   client_secret =
   token = {"access_token":"ya29.GlsyBNeHGVXOwiKz4f5qu9R-IVVV7mgalSGVTK0v_snzHuKU3YpAs3D0AKLbR5pkl_jqHqrNSA5l4regTfgHl7GWe7vpj5SPGLnKOvp_eEQ24GgrZdbSb9Flks","token_type":"Bearer","refresh_token":"1/_X4omasTIoXnO4k9SGcmri-S4XDTsBxA2MzxgrrxmYTU0nJZ3Os_N3lqzhyUqZo","expiry":"2017-04-19T16:15:32.557926381-07:00"}
   --------------------
   y) Yes this is OK
   e) Edit this remote
   d) Delete this remote
   y/e/d> y
   ```
   Q9: Quit.
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
   ```

4. Verify that the configuration was written:
   ```
   grep gDrive /data/users/yourusername/.config/rclone/rclone.config
   ```
   should return:
   ```
   [gDrive]
   ```
You should now be able to access your Google Drive account through RClone.  If that is not the case and you are out of ideas, contact me for help.

### RClone Short Command Tutorial and Examples

The Google Drive alias name we created in the above RClone configuration is ```gDrive```.  We will reference it throughout this section.  Note: All RClone commands begin with `rclone`, ie:

#### `rclone ls gDrive:` 
Lists all of your Google Drive files.

#### `rclone lsd gDrive:` 
Lists all of your top level Google Drive directories.  Analogous to `ls -d */` in Linux.

#### `rclone mkdir gDrive:fooism` 
Creates a directory in your Google Drive 'home' directory called _fooism_.

#### `rclone copy testfile.dat gDrive:fooism` 
Copies the file *testfile.dat* to the Google Drive folder _fooism_.

#### `rclone copy gDrive:fooism/testfile.dat /pub/YourHPClogin`
Copies the file *testfile.dat* from Google Drive folder _fooism_ to your HPC `/pub` folder on HPC.

#### `rclone sync ~/ gDrive:fooism --drive-use-trash`
**Deletes or overwrites all content** of the Google Drive folder *fooism* that does not match the content of your home directory.  Make sure that the destination directory (in this case *fooism*) is not being written to by other sources since those files will be deleted or overwritten by the sync.  When doing manual backups it is strongly encouraged the sync option `--drive-use-trash` is always used.  The are sent to the Google Drive trash folder, for a certain period of time, before being deleted permanently.  That allows for some file recovery, in case a sync deletes needed files.

### Quick Manual Cloud Backup

** You must be on the interactive node to do manual cloud backups. **

First check that there are no other rclone instances you are running:
`ps aux | grep rclone`
If there are, backup is still running.  Check the log files to see the state of the backup.  To kill the backup execute `kill -9 [PID]`, where `[PID]` is the process ID of the rclone session you have been running. 

Create Google Drive backup directories (one to save everything in from your /pub/yourHPCLogin and /data/users/yourHPCLogin:
`
module purge
module load rclone
rclone mkdir gDrive:uci_hpc_pubdir_backup
rclone mkdir gDrive:uci_hpc_homedir_backup
`
The biggest issue with doing manual backups yourself is the time it takes for the backup to complete.  To ensure the backup takes place after you log out or lose connection to HPC, create a short bash script called *backup_to_gDrive.sh* as follows:
```
# Backup all of your /pub/yourHPCLogin
setsid rclone copy -vv --include-from pubDirFilesToSave.txt --exclude-from filesToExclude.txt \
   /pub/yourHPCLogin gDrive:uci_hpc_pubdir_backup --dump-filters --log-file ~/hpc_pubdir_cloud_backup.log \
   --transfers=32 --checkers=16 --drive-chunk-size=16384k --drive-upload-cutoff=16384k --drive-use-trash &>/dev/null

# Backup all of your /data/users/yourHPCLogin
setsid rclone copy -vv --include-from homeDirFilesToSave.txt --exclude-from filesToExclude.txt \
   /data/users/yourHPCLogin gDrive:uci_hpc_homedir_backup --dump-filters --log-file ~/hpc_homedir_cloud_backup.log \
   --transfers=32 --checkers=16 --drive-chunk-size=16384k --drive-upload-cutoff=16384k --drive-use-trash &>/dev/null
```
`setsid` - makes sure rclone runs even if HPC connection lost
`pub[home]DirFilesToSave.txt` - list of files or patterns (globs)

*pubDirFilesToSave.txt* example that saves everything in your /pub/yourHPCLogin dir:

   ```   
      /**
   ```

*homeDirFilesToSave.txt* example to save everything in my /data/users/yourHPCLogin dir:

   ```
      /**
   ```

Yes, `/**` is that is needed in pub(home)DirFilesToSave.txt if you want to save everything in your */pub* and */data/users* folder.

If you are only interested in sub-folder(s) of */pub/yourHPCLogin* such as */pub/yourHPCLogin/Work* and */pub/yourHPCLogin/UHEMuons*, include the following lines, in **decending** order to importance in your pubDirFilesToSave.txt:

```
Work/**
UHEMuons/**
```

Similarly if you are only interested in sub-folder(s) of */data/users/yourHPCLogin* such as */data/users/yourHPCLogin/MCOutput* and all .dat files in */data/users/yourHPCLogin* you would include the following lines in your *homeDirFilesToSave.txt*:

```
MCOutput/**
/*.dat
```

*filesToExclude.txt* should contain rules or specific files to be excluded.  For example, if you do not want emacs backup files ending in *~* or core dumps, your *filesToExclude.txt* will contain:
```
*~
core.*
```

*hpc_homedir_cloud_backup.log* and *hpc_pubdir_cloud_backup.log* are log files that will contain rclone's progress.  Any errors will also be logged there.

*`--transfers=32 --checkers=16 --drive-chunk-size=16384k --drive-upload-cutoff=16384k`* are settings optimized for large file transfers.  There is no need to change the settings for smaller file transfers.

### Automatic Backups to Google Drive from HPC

After configuring RClone as described in the [RClone Configuration][#rclone-configuration] section above, you need to follow the steps outlined below in order to set up automatic Google Drive backups from the **interactive** node (compute-1-13) **only**.

1.  Create *.hpc_cloud_backup* dir:
```
cd /data/users/yourHPCLogin`
mkdir .hpc_cloud_backup`
```
2.  Decide on the files and dirs you want to backup:
```
cd .hpc_cloud_backup`
vim/emacs/nano backup`
```
Example: to backup your entire home directory and all of put add the following two lines to the file *backup*:
```
/data/users/yourUCILogin
/pub/yourUCILogin
```

3.  Decide on files and dirs you want to **exclude** from backup.  In */data/users/yourUCILogin/.hpc_cloud_backup* do:
```
vim/emacs/nano exclude
```
Example: you may want to exclude all hidden files (ones that start with `.`) from being backuped up, since they frequently contain tockens and passwords include the following line in the file *exclude*:
```
.*
```
To also exclude all files in directories starting with `.` add the following line to *exclude*:
```
.*
.*/**
```

Now you are ready to start backing up by executing (**on interactive node only**):
```
cloudBackup.py
```

Check that *cloudBackup.py* is running:
```
ps x | grep cloudBackup.py
```

There are a number of options that you can specify or accept the defaults.  To see what the defaults are, type:
```
cloudBackup.py -h
```

Note: Setting *dt* to 0 will running the backup once and exit.  To do so execute:
```
cloudBackup.py -dt 0
```

There are a number of log files to pay attention to:
*/data/users/yourUCILogin/.hpc_cloud_backup/logs/cloudbackup.log*
*/data/users/jtatar/.hpc_cloud_backup/logs/sessions/RCloneCmdLine_{#}.log*

**Before** starting *cloudBackup.py* make sure there is no pid file from a previous backup session that did not exit gracefully.  If there is, remove it:
```
rm /data/users/jtatar/.hpc_cloud_backup/cloudbackup.pid
```

**NOTE**:  Make sure you have read/write permissions of **all directories** you are trying to backup.  If *cloudBackup.py* tries to backup a directory you have no proper permissions for, it will exit.


### Retreiving Backup from Cloud to HPC

### Archival Storage
