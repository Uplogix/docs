# Clarifications

FIPS 140-2 is the Federal Information Processing Standard for encryption of sensitive information using the NIST certified standard. 

## FIPS mode for the Uplogix Control Center

Uplogix uses NIST validated encryption libraries on the Uplogix Control Center (UCC) that are tested by NIST in conjunction with the Uplogix Local Manager (Certificate #2140). NIST does not separately validate the identical libraries on the UCC since the Uplogix FIPS 140-2 encryption boundary is drawn around those libraries.

The functional change with FIPS mode for the UCC is replacing the default SSL certificates with specific SSL certificates from an organization’s private key infrastructure. (PKI) This will prohibit Local Managers and user browsers without certificates in the “Trusted” chain from communicating with the UCC.

> Note: FIPS mode on the UCC additionally restricts the unusual configuration choice of inadequate cryptography or enabling “telnet”, which are already disabled by default. If SMTP is configured to use SSL/TLS, it must use TLS 1.0 with AES or Triple-DES.

## Initial UCC setup

This configuration guide assumes initial UCC setup for network addressing and default password set has been previously completed. 

## Certificates (PKI)

The UCC will need two distinct certificates issued by a customer's trusted certificate authority to enable communication with 1) end-user's web browsers and 2) Uplogix Local Managers. The enduser's web browser will communicate with the UCC on port 443 using HTTPS; the UCC will identify itself with the "www" certificate. Local Managers will communicate with the UCC on port 8443 using web service requests secured by HTTPS with the "heartbeat" certificate.

The certificate request and installation must be generated using the command line interface of the UCC using standard Linux tools from the administrator user (emsadmin) with ‘root’ privileges.

Proper installation will require four artifacts:
- Certificate for communication between the end-user’s web browsers and the UCC
- Certificate for communication between the Uplogix Local Manager and the UCC
- An intermediate Certificate Authority (CA) used to sign the "www" certificate
- A CA that is trusted by the UCC to sign Local Manager certificates

## Certificate requests to be submitted to the PKI administrator to be issued

The certificate requests and installation must be generated using the command line interface of the UCC using standard Linux tools from the administrator user (emsadmin) with ‘root’ privileges. These are unique for the control center host.

The UCC certificates issued should be of "SSL Server" type and signed with SHA2 (SHA-256, SHA-384, or SHA-512).

### Server certificate – HTTPS

Selected as the “www” element in the command line tools, this certificate is used to uniquely identify the UCC to browsers on port TCP/443. It can be either a 2048, 3072, or 4096-bit RSA certificate.

### Server certificate – Heartbeat

Selected as the “heartbeat” element in command line tools, this certificate is used to uniquely identify the UCC to Local Managers on port TCP/8443. It can be either a 2048, 3072, or 4096-bit RSA certificate.

> Note: The Server certificate – Heartbeat is imported into a Local Manager using **config system crypto certificate management** command.

## Certificates from PKI administrator to be imported on the UCC command line

These certificates are general in nature and used throughout the PKI to establish trust. They will only be imported into the UCC.

### Local Manager CA certificate

This certificate is the one used to sign a Local Manager's "client" certificate. The UCC will trust any Local Manager certificate that is signed by this CA.

### Intermediate CA certificate

This is used to establish trust for browser clients. It can be between 1024 and 4096-bits in length. Most CAs do not sign their certificates with a self-signed root CA that an end user's browser will trust. Instead, the PKI administrator will have their root CA certificate sign an intermediate CA certificate which will then sign the certificates issued to the CA's customers. Importing the intermediate CA certificates into the UCC allows the UCC to present those intermediates to the end-user so the browser can then verify the entire chain of certificates.

> Note: In many deployments these intermediate CA certificates will be the same ones used to create
the Local Manager certificates.

# Implementation

These steps must be completed from the UCC command line interface (SSH or serial console) logged in as emsadmin and promoted to root access using the SUDO command.

## Steps to complete before submission to PKI administrator

Uplogix includes FIPS verified encryption libraries on the Uplogix Control Center (UCC) that are utilized even when FIPS mode is not indicated. This document will focus on replacing only the default certificates shipped with the software so that ONLY the trust relationship between designated systems will succeed.


### Login as emsadmin and become root

As with all OS-level configuration, you must first log into the UCC via SSH or console and [become root](http://uplogix.com/docs/control-center-user-guide/managing-the-control-center/becoming-root).

### Stop Web Services

```
[root@UplogixControlCenter ~]# service tomcat stop
[root@UplogixControlCenter ~]# Stopping Uplogix Control Center: [ OK ]
[root@UplogixControlCenter ~]#
```

### Change to the database user to execute specific database commands

```
[root@UplogixControlCenter ~]# su - oracle
[oracle@UplogixControlCenter ~]$
```

### Use the SQLPLUS utility to make the initial table changes

```
[oracle@UplogixControlCenter ~]$ sqlplus embassy_a

SQL*Plus: Release 10.1.0.2.0 - Production on Wed Apr 17 21:00:32 2019

Copyright (c) 1982, 2004, Oracle.  All rights reserved.

Enter password:

Connected to:
Oracle Database 10g Enterprise Edition Release 10.1.0.2.0 - Production
With the Partitioning, OLAP and Data Mining options

21:00:35 EMBASSY_A> update embassy_settings set fips_enabled = 1;
1 row updated.
21:00:35 EMBASSY_A> commit;
Commit complete.
21:00:35 EMBASSY_A> exit
Disconnected from Oracle Database 10g Enterprise Edition Release 10.1.0.2.0 - Production
With the Partitioning, OLAP and Data Mining options
[oracle@UplogixControlCenter ~]$ exit
[root@UplogixControlCenter ~]# 
```

### Generate the signing request for the Heartbeat Service Instance (8443)

Substitue your own info in the required fields. 

```
[root@UplogixControlCenter ~]# /uplogix/embassy/scripts/generateCertificateSigningRequest.sh
Initializing crypto.
Common Name: 203.0.113.100 OR FQDN
Organizational unit: Uplogix-heartbeat
Organization: Uplogix
City: Austin
State/Province/Region: Texas
2-letter country code: US
Country code 'US' is United States.
Email address (optional):
Other Attributes:
Generate? (y/n): y
Generating new 2048-bit key pair.
-----BEGIN NEW CERTIFICATE REQUEST-----
MIICuzCCAaMCAQAwdjELMAkGA1UEBhMCVVMxDjAMBgNVBAgTBVRleGFzMQ8wDQYD
VQQHEwZBdXN0aW4xEDAOBgNVBAoTB1VwbG9naXgxHDAaBgNVBAsTE1Rlc3RDaGFp
bi1oZWFydGJlYXQxFjAUBgNVBAMTDTE3Mi4zMC4xMTEuNzIwggEiMA0GCSqGSIb3
DQEBAQUAA4IBDwAwggeKAoIBAQC8M6lsh/wwAyvWGMIgzwQrlz/A7xvDXF/KNfUH
fgevHP44gzr1+GNQ5h0qbV/YP9dLHRYwrn4ell50uKjMyzISVEEYsErydAgT+Rdb
p4a05ZZRb4GcXWp8lXZucFHLGKZua79HWRJRU0gXVnwSFeFCzu0XH1RSSI/JJi5W
oVEifTZnVcjjPRKuaFtdcyNsSCvq2ovUd2hBd4P/ObCJbmhuTsfau1Ta8YjRXQdx
5rmyIyjzEQG4dCyur76hkesbOTFI4XGJoOEfQw5fcMLWC8JBAsRUIo8WD9TkWtf1
Q67gmzKhYEHmKywOz7NsOuvf5ELSUi9pbrQpO5tYdm8RMUGfAgMBAAGgADANBgkq
hkiG9w0BAQsFAAOCAQEAFHCCeAhFEItzO/luXa0MzxSjGyjStOhVd56lHdKPIHo5
9z/iAOn9H/sOMfB181+tkQVyi2N9gmKwldf/GRCHcck/hVDhzEPf9aidc6h9xlLP
ecC+A6M6RA4bj9v+ft3oQ4G1IAKp4b0KMhXKD5d2m6Ozw1EpHIoDOHvL0XgMPG3C
dxBNvZEU/C3qsDpVKhjuJNClXAPSk3UajI5L2gSWAgcesvljTDLNrsadmOQOZWEe
mDcy/53SQJBq7OjHgEDWK05JBkYnfeJhNycpUevkVjglUA87pvNgpJc2DLeDMlnP
Configuration Guide for Uplogix Control Center FIPS mode 6
/pPhmLSzkPxt+R0XLkncJA5FlmIc7l4QAAsy9oNU2g==
-----END NEW CERTIFICATE REQUEST-----
```

