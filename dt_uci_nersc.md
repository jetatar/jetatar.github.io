# Data Transfer Overview

RCIC provides a number of tools for UCI users to be able to move their data in and out of UCI.  For data transfer consultation
please contact Joulien Tatar (jtatar@uci.edu).

The Data Transfer Nodes (DTN) are dedicated UCI servers that are optimized for fast data transfers.  These DTNs are on UCI's dedicated 10Gb Lightpath network and part of the Pacific Research Platform (PRP).  The PRP is an initiative to connect research institutions (mostly) on the west coast to the nationwide Science DMZ network.

# Configuration

The data transfer node is:

* fiona.oit.uci.edu 

It is located at the UCI data center and setup for interactive use.  The FIONA DTN is **not** on UCI's general network, UCINet, but it can access any UCINet host and vice versa.  The DTN has a 10Gb ethernet link but no physical link to the HPC or Greenplanet clusters' filesystems.

# Access

UCI researchers need to request access to the DTN (jtatar@uci.edu) and provide information on what research related needs they will utilize the network for.  For interactive use, the DTN can be accessed via SSH.  For data transfer, the DTN supports the GridFTP services.  The DTN also setup as a Globus endpoint that can be found on Globus online by searching for **UCI#DTN**.

# References
http://www.oit.uci.edu/wp-content/uploads/UCI-Lightpath-Access-Policy.pdf
http://sites.uci.edu/rcna/uci-lightpath/

