# Dockerfile

When building containers within docker, we need to copy the certificate into the container and into the appropriate location. 

In this Dockerfile below, we assume that the custom Root CA certificate bundle (ca-cert-bundle.pem) is in the same directory as the Dockerfile.

* Add the Root CA Certificate to the container
```
ADD ca-cert-bundle.pem /tmp/ca-cert-bundle.pem
```
* Find the location of the certificate directory. Copy the ca-cert-bundle.pem file into this directory. Run update-ca-certificates.

***Note:** The following command is specific to Debian-based systems.*
```
RUN CERT_DIR=(openssl version -d | cut -f2 -d \")/certs ; cp /tmp/ca-cert-bundle.pem $CERT_DIR ; update-ca-certificates ;
```
