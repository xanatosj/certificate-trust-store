# Adding SSL Decryption/MITM certificates to application-specific trust stores for common apps

<details>
<summary>Azure CLI (Microsoft)</summary>
To add a custom root into the Azure CLI trust store, add the PEM to the following file.

> C:\Program Files (x86)\Microsoft SDKs\Azure\CLI2\Lib\site-packages\certifi\cacert.pem

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
<summary>Snowflake ODBC Driver</summary>
Snowflake can be configured to connect to the data warehouse over https; to allow this via proxy, replace the PEM file under C:\Program Files\Snowflake ODBC Driver\etc with your custom CA PEM file.

> C:\Program Files\Snowflake ODBC Driver\etc

* If the JRE directory is not present, use the JBR directory instead (Android Studio Version dependant).
* Ensure that you specify the full path to the Android Studio Keystore.
</details>
