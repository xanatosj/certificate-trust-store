# Deploying CA Certificates

## Why is this needed? 
Applications are not typically aware of upstream devices/services that perform SSL/TLS decryption of traffic. When a connection attempt is made and the device/application is unaware of this certificate, it doesn’t allow for the secure handshake to complete.  Updating the trusted certificate store for the application removes the requirement for either removing the traffic from the scope of decryption and/or instructing tools to bypass certificate validation for secure connections.

## Assumption
* The Root CA is already available in base64 format (pem).
* All traffic is tunneled through the solution that is performing decryption. (i.e. no SSL/TLS decryption exclusions)
* To get a cacert.pem bundle, you can download it from here https://curl.se/ca/cacert.pem 

## Disclaimer
This document is subject to change due to applications changing the ways they potentially use certificates.

## Tools/Application list with Guides
[AWS CLI (Amazon Web Services)](https://github.com/xanatosj/certificate-trust-store/blob/main/AWS/AWSCLI.md)

[Azure CLI](https://github.com/xanatosj/certificate-trust-store/blob/main/AzureCLI/AzureCLI.md)

<details>
<summary>cURL</summary>
Create a certificate bundle that includes the Root CA certificate and the public Certificate Authorities

Set cacert config option

> echo "cacert=/path/to/ca-cert-bundle.pem" >> $HOME/.curlrc

Set CURL_CA_BUNDLE environment variable

> echo "export CURL_CA_BUNDLE=/path/to/ca-cert-bundle.pem" >> $HOME/.bashrc

Set SSL_CERT_FILE environment variable

> echo "export SSL_CERT_FILE=/path/to/ca-cert-bundle.pem" >> $HOME/.bashrc

</details>


<details>
<summary>Docker</summary>
When building containers within docker, we need to copy the certificate into the container and into the appropriate location. 

> \# Previous Dockerfile lines \
> \# Add the Root CA Certificate to the container \
> ADD ca-cert-bundle.pem /tmp/ca-cert-bundle.pem \
> \# Find the location of the certificate directory. Copy the ca-cert-bundle.pem file into this directory. Run update-ca-certificates. \ 
> RUN CERT_DIR=(openssl version -d | cut -f2 -d \")/certs ; cp /tmp/ca-cert-bundle.pem $CERT_DIR ; update-ca-certificates ; \
> \# More Dockerfile lines \


</details>

<details>
<summary>Firefox (Mozilla)</summary>
Configure Mozilla Firefox to use the Windows root certificate store.

* In the browser, type "about:config" in the browser.  When the caution prompt appears, select Accept the Risk and Continue.
> about:config
* In the config search bar, type "security.enterprise_roots.enabled".  Change the option from False to True
> security.enterprise_roots.enabled

</details>

<details>
<summary>Intune (Microsoft)</summary>
Follow Microsoft provisioning guide
 
https://learn.microsoft.com/en-us/intune/intune-service/protect/certificates-trusted-root

</details>



[Java](https://github.com/xanatosj/certificate-trust-store/blob/main/Java/Java.md)


<details>
<summary>npm</summary>
 
1) Create a PEM file containing the root and intermediate certificates

2) Run npm command, setting the cafile
> npm config set cafile path/of/ca-bundle.pem
</details>

<details>
<summary>PHP</summary>
 
Inside php.ini specify path to the certs.  Create the following entry:
> openssl.cafile=/path/to/cacert.pem

_Restart of web services may be needed_
</details>

<details>
<summary>Python</summary> 
Use one of the following methods for Python via PIP.
<details>
 <summary> Adding the custom certificate</summary>
<details>
<summary>MacOS/Linux</summary>

1) Create a directory to host the CA Cert Bundle.  Move the cert bundle to that location
> mkdir ~/ca_certs
> mv ~/Downloads/custom-ca-bundle.pem ~/ca_certs
2) Add cert bundle to python to trust the cert chain

> pip config set global.cert ~/ca_certs
</details>
<details>
<summary>Windows</summary>
 
1) Create a new directory and move the bundle to C:\ drive.
 
2) Add certificate bundle to python trust store (command below via Powershell)
> mv $env:HOMEPATH\Downloads\custom-ca-bundle.pem $env:APPDATA

> pip config set global.cert $env:APPDATA\custom-ca-bundle.pem 
</details>
</details>
<details>
<summary>Set via the environment variables</summary>
Run the following commands to set the SSL_CERT_FILE option to use the (downloaded) cert bundle
 
> export CERT_PATH=/etc/ssl/certs/SSLDecrypt.pem
> 
> export CERT_DIR=/etc/ssl/certs/
> 
> export SSL_CERT_FILE=${CERT_PATH}
> 
> export SSL_CERT_DIR=${CERT_DIR}
> 
> export REQUESTS_CA_BUNDLE=${CERT_PATH} 
</details>
</details>

<details>
<summary>Rust (Linux)</summary>
Use Rust to add the decryption root ca to the Linux Trust store

1) Place root certificate(s) in the following directory
> /usr/local/share/ca-certificates/
2) Update the CA store via CLI.  Note - Sudo permissions required

 > sudo update-ca-certificates


</details>


<details>
<summary>Snowflake ODBC Driver</summary>
Snowflake can be configured to connect to the data warehouse over https; to allow this via proxy, replace the PEM file under C:\Program Files\Snowflake ODBC Driver\etc with your custom CA PEM file.

> C:\Program Files\Snowflake ODBC Driver\etc

* If the JRE directory is not present, use the JBR directory instead (Android Studio Version dependant).
* Ensure that you specify the full path to the Android Studio Keystore.
</details>


<details>
<summary>VSCode</summary>
 
By default VSCode does not use the built-in certificate store (Windows) or the System Keychain (macOS); VSCode needs to have a plugin installed to instruct it to use the certificate store (Windows), or System Keychain (macOS)


_**macOS**_

This is a custom plugin at the VSCode Marketplace - [Mac CA VSCode - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=linhmtran168.mac-ca-vscode)

_**Windows**_

This is a custom plugin at the VSCode Marketplace - [win-ca - Visual Studio Marketplace ] (https://marketplace.visualstudio.com/items?itemName=ukoloff.win-ca)
</details>
