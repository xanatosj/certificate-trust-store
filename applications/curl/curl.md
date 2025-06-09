# cURL

Create a certificate bundle that includes the Root CA certificate and the public Certificate Authorities

* Set cacert config option
```
echo "cacert=<Path to Certificate>/ca-cert-bundle.pem" >> $HOME/.curlrc
```
* Set CURL_CA_BUNDLE environment variable
```
echo "export CURL_CA_BUNDLE=<Path to Certificate>/ca-cert-bundle.pem" >> $HOME/.bashrc
```
* Set SSL_CERT_FILE environment variable
```
echo "export SSL_CERT_FILE=<Path to Certificate>/ca-cert-bundle.pem" >> $HOME/.bashrc
```
