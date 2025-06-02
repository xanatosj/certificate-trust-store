# Adding SSL Decryption/MITM certificates to application-specific trust stores for common apps
<details>
<summary>Snowflake ODBC Driver</summary>
Replace the PEM file under C:\Program Files\Snowflake ODBC Driver\etc with your custom CA PEM file.

* Ensure that you specify the full path to the Android Studio Keystore.

* In later versions of Android Studio (Android Studio version 2024.1.1 Patch 1 or later), the JRE directory might not be present; use the JBR directory instead.
</details>
<details>
<summary>Python via PIP (In Progress)</summary> Python
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
