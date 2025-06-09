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
[AWS CLI (Amazon Web Services)](https://github.com/xanatosj/certificate-trust-store/blob/main/AWS/AWSCLI.md)

[Azure CLI](https://github.com/xanatosj/certificate-trust-store/blob/main/AzureCLI/AzureCLI.md)

[cURL](https://github.com/xanatosj/certificate-trust-store/blob/main/curl/curl.md)

[Docker](https://github.com/xanatosj/certificate-trust-store/blob/main/docker/dockerfile.md)

[Firefox](https://github.com/xanatosj/certificate-trust-store/blob/main/firefox/firefox.md)

[GIT](https://github.com/xanatosj/certificate-trust-store/blob/main/git/git.md)

[Intune Provisioning Guide](https://learn.microsoft.com/en-us/intune/intune-service/protect/certificates-trusted-root)

[Java](https://github.com/xanatosj/certificate-trust-store/blob/main/Java/Java.md)

[Minikube](https://minikube.sigs.k8s.io/docs/handbook/vpn_and_proxy/#x509-certificate-signed-by-unknown-authority)

[npm](https://github.com/xanatosj/certificate-trust-store/blob/main/npm/npm.md)

[PHP](https://github.com/xanatosj/certificate-trust-store/blob/main/php/php.md)

[Python](https://github.com/xanatosj/certificate-trust-store/blob/main/python/python.md)

[Rust](https://github.com/xanatosj/certificate-trust-store/blob/main/rust/rust.md)

[Snowflake ODBC Driver](https://github.com/xanatosj/certificate-trust-store/blob/main/snowflake/snowflake.md)

[VSCode](https://github.com/xanatosj/certificate-trust-store/blob/main/VSCode/VSCode.md)

[wget](https://github.com/xanatosj/certificate-trust-store/blob/main/wget/wget.md)
