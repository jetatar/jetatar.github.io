Logging In:

Open a new tab/window on your favorite browser __on your own machine__ and enter the UCI HPC Jupyterhub URL: https://hpc.oit.uci.edu:8000

You should see the following Jupyterhub login page where you should enter your cluster username and password:
![JuputerhubLogin](https://github.com/jetatar/Docs/blob/master/jupyterhublogin.png?raw=true)

At some point during or right after login you may get warning similar to this:
![JuputerhubStartNotebook](https://github.com/jetatar/Docs/blob/master/JupyterhubloginWarning1.png?raw=true)
Click on Advanced.  You should see a screen similar to this:
![JuputerhubStartNotebook](https://github.com/jetatar/Docs/blob/master/JupyterhubloginWarning2.png?raw=true)
Click on `Proceed to 128.200.84.31 (unsafe)`. 
If you are able to successfully login, you should see the following screen (except no Admin button for regular users).  Click on the "Start My Server" button in order to start a Jupyterhub (Single User) Notebook:
![JuputerhubStartNotebook](https://github.com/jetatar/Docs/blob/master/JupyterStartAServer.png?raw=true)
Waiting up to (but not exceeding) 2 min after clicking the link, you should see a page with a file browser menu:
![JuputerhubStartNotebook](https://github.com/jetatar/Docs/blob/master/JupyterFilesBrowser.png?raw=true)
Jupyterhub has been configured such that user's Juputerhub Single User Instances are all lauched on a selected queue where each user has been allocated the same system resources.
![JuputerhubStartNotebook](https://github.com/jetatar/Docs/blob/master/JupyterSingleNotebooksQueue.png?raw=true)



If you are able to successfully login, you should see the following screen (except no Admin button):


UCI's Jupyterhub Instance is running at: https://hpc.oit.uci.edu:8000.  If you try to connect from outside the UCI network, you will have first login to the UCI VPN pool before you are able to access HPC's Jupyterhub page.
