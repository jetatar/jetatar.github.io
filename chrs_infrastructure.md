# Overview

![Sketch](https://github.com/jetatar/Docs/blob/master/CHRS_QuickSketch.jpg?raw=true)

# Details

The two frontend servers chrs-web1 and chrs-web2 were purchased and installed.  The hardware specifications are:

![Web servers](https://github.com/jetatar/Docs/blob/master/chrs_web_servers.png?raw=true)

They were intalled in the data center in CHRS' personal rack.  The web servers were configured with Apache and setup to be mirrored in case failover needs to kick in when one server goes down.  The web servers are on Lightpath for 10Gbit connectivity.

Two database servers with the specifications below have been bought and installed in the data center.  They have been also setup for failover in case one fails. Garr Updegraff is still working on transferring the massive databases the group had on their old servers.  There were multiple instances of the same database running on those servers.  They were not optimized for performance at all.  Due to the complexity of the MySQL databases.

![Database servers](https://github.com/jetatar/Docs/blob/master/chrs_database.png?raw=true)



![Compute nodes](https://github.com/jetatar/Docs/blob/master/chrs_compute.png?raw=true)

A 500TB JBOD with the configuration below was collocated in the datacenter with the new compute nodes.  The JBOD is partially polulated on per need basis.  The server was setup to run ZFS.  The JBOD will be primarily used for archival storage.

![JBOD](https://github.com/jetatar/Docs/blob/master/chrs_jbod.png?raw=true)
