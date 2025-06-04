# Common OpenSSL Commands

## Convert PFX/PKCS12 to PEM

> openssl pkcs12 -in yourcert.p12 -out yourcert.pem -nodes

## Convert PFX/PKCX12 to CRT
 > openssl pkcs12 -in filename.p12 -clcerts -nokeys -out filename.crt

## Convert PEM to DER

> openssl x509 -in yourcert.pem -inform pem -out yourcert.der -outform der

