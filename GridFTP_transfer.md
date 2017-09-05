# GridFTP Data Transfer

GridFTP is an iteration of the FTP protocol, optimized for high-bandwidth grid computing environments.  GridFTP allows users to perform parallel transfers.  It is command line based, but there is also an online client called Globus that provides easy to use point and click interface that adds reliability and automatically optimizes transfers for performance.  It is highly recommended users use Globus over the command line based GridFTP.

# Transferring Data To and From the UCI DTN Using GridFTP clients

GridFTP is available on the UCI FIONA DTN: fiona.oit.uci.edu

## Using globus-url-copy
The basic GridFTP client, distributed with the Globus Toolkit, is called **globus-url-copy**.  It is command line based and it is not interactive.  It allows only one file transfer at a time.  **globus-url-copy** is installed on the UCI FIONA DTN.  The following commands are to be executed from the FIONA.

### Get a Grid certificate
A GridFTP certificate is a type of digital ID (an X.509 digital certificate).  It is issued by a Certification Authority.  For all DTN FIONA users the Certification Authority is the UCI RCIC.  The certificate uniquely identifies you (the GridFTP user) for all GridFTP transfers.  To start the process, execute the following command and set a certificate password, when prompted.

```
grid-cert-request
```

Next, **inform the RCIC staff (ie Joulien Tatar) that you have a certificate you would like to have approved**.  The RCIC staff representative will have to sign off on your certificate, thus validating it.  Your certificate is invalid prior to validation.

### Initialize a proxy certificate


# References
http://toolkit.globus.org/toolkit/docs/latest-stable/gridftp/
