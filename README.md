# Deploying CA Certificates to Applications

## Why is this needed? 
Applications are not typically aware of upstream devices/services that perform SSL/TLS decryption of traffic. When a connection attempt is made and the device/application is unaware of this certificate, it doesn’t allow for the secure handshake to complete.  Updating the trusted certificate store for the application removes the requirement for either removing the traffic from the scope of decryption and/or instructing tools to bypass certificate validation for secure connections.

## Creating a certificate bundle

To create a certificate bundle that includes both the public Certificate Authorities and the corporate Certificate authority. 

* Download the certificate bundle from [https://curl.se/ca/cacert.pem](https://curl.se/ca/cacert.pem) 

* Append the Root CA Certificate(s) to the cacert.pem file that you downloaded. It is recommended to save this as a new file name: ```ca-cert-bundle.pem```. 

## Disclaimer
This document is subject to change due to applications changing the ways they potentially use certificates.

## Application Guide List
[AWS CLI (Amazon Web Services)](applications/AWS/AWSCLI.md)

[Azure CLI](applications/AzureCLI/AzureCLI.md)

[cURL](applications/curl/curl.md)

[Docker](applications/docker/dockerfile.md)

[Firefox](applications/firefox/firefox.md)

[GIT](applications/git/git.md)

[Intune Provisioning Guide](https://learn.microsoft.com/en-us/intune/intune-service/protect/certificates-trusted-root)

[Java](applications/Java/Java.md)

[Minikube](https://minikube.sigs.k8s.io/docs/handbook/vpn_and_proxy/#x509-certificate-signed-by-unknown-authority)

[npm](applications/npm/npm.md)

[PHP](applications/php/php.md)

[Python](applications/python/python.md)

[Rust](applications/rust/rust.md)

[Snowflake ODBC Driver](applications/snowflake/snowflake.md)

[VSCode](applications/VSCode/VSCode.md)

[wget](applications/wget/wget.md)
