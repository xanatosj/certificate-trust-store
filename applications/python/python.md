# Python

## PIP
### SSL_CERT_FILE environment variable
Upload the Root CA certificate to the /etc/ssl/certs directory.
```
export CERT_PATH=/etc/ssl/certs/ca-cert-bundle.pem
export CERT_DIR=/etc/ssl/certs/
export SSL_CERT_FILE=${CERT_PATH} 
export SSL_CERT_DIR=${CERT_DIR}
export REQUESTS_CA_BUNDLE=${CERT_PATH} 
```
### Patching PIP to use system certificates
The ```pip-system-certs``` package can be used to patch PIP and the requests at runtime to use certificates from the default system store in preference to the bundled certificates CA.

```
pip install -trusted-host files.pythonhosted.org pip_system_certs
```
After this command is run, PIP will use the system certificates that are trusted by your OS. It will also get the requests library and other packages that use requests to trust the system certificates.
## Requests
Requests automatically search for any valid certificate in the REQUESTS_CA_BUNDLE environment variable.\
* Linux(bash)
```
echo "export REQUESTS_CA_BUNDLE=<Path to Certificate>/ca-cert-bundle.pem" >> $HOME/.bash_profile
```
* macOS (bash)
```
echo "export REQUESTS_CA_BUNDLE=<Path to Certificate>/ca-cert-bundle.pem" >> $HOME/.bash_profile
```
* macOS (zsh)
```
echo "export REQUESTS_CA_BUNDLE=<Path to Certificate>/ca-cert-bundle.pem" >> $HOME/.zshrc
```
* Windows (powershell)
```
[System.Environment]::SetEnvironmentVariable("REQUESTS_CA_BUNDLE", "<Path to Certificate>\ca-cert-bundle.pem", "Machine")
```
