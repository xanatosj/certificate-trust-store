# Git

## Git on Windows
In PowerShell, run the following command:

```git config -l```

In the output, look for the following reference:\
```http.sslcainfo=C:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt```

The http.sslcainfo defines the CA Certificate store. To append the PEM certificate to the CA bundle, update http.sslcainfo. \
~~```gc /path/to/your/custom_ca_bundle.pem | ac $(git config --get http.sslcainfo)```~~
```powershell
$git_ca_bundle = git config --get http.sslcainfo
Get-Content -Path "/path/to/your/custom_ca_bundle.pem" | Add-Content -Path $git_ca_bundle
```

## Git on Mac and Linux
To configure Git to trust a new root certifcate certificate, run the following command:\
~~```git config --global http.sslcainfo /path/to/your/custom_ca_bundle.pem```~~
```bash
cat /path/to/your/custom_ca_bundle.pem >> $(git config --get http.sslcainfo)
```

