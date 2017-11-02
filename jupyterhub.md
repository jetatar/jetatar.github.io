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
If you have a .ipynb file you want to work on, select it, and a new tab should open with the content of your Notebook or start a new Notebook by clicking on the 'New' button on the top right side of the Jupyterhub page:
![JuputerhubStartNotebook](https://github.com/jetatar/Docs/blob/master/JupyterNoteBookHelloWorld.png?raw=true)


To stop the Notebook press the `Control Panel` button at the top right corner of the Notebook window.  Then you should see the following buttons:  
![JuputerhubStartNotebook](https://github.com/jetatar/Docs/blob/master/JupyterStopNotebook.png?raw=true)

Press the red `Stop My Server` button to stop your Notebook server.  Please note that if you don't stop your server when you no longer need a Jupyter Notebook instance, your Notebook will wastefully continue to occupy a core on the Jupyterhub queue.  Please don't forget to __stop your server__.  We reserve the right to delete your job if the resources you occupy are unused for an extended period of time.


If you are able to successfully login, you should see the following screen (except no Admin button):


UCI's Jupyterhub Instance is running at: https://hpc.oit.uci.edu:8000.  If you try to connect from outside the UCI network, you will have first login to the UCI VPN pool before you are able to access HPC's Jupyterhub page.
