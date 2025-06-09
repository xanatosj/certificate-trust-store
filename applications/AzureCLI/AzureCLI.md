# Azure CLI


## Configure the ```REQUESTS_CA_BUNDLE``` Environment Variable

Set the ```REQUESTS_CA_BUNDLE environment``` variable to the full path of your PEM-encoded custom CA certificate bundle file.

**Linux/macOS (for current session):** \
```export REQUESTS_CA_BUNDLE="/path/to/your/custom_ca_bundle.pem"``` \
**Windows (Command Prompt - for current session):** \
```set REQUESTS_CA_BUNDLE="C:\path\to\your\custom_ca_bundle.pem"``` \
**Windows (PowerShell - for current session):** \
```$env:REQUESTS_CA_BUNDLE="C:\path\to\your\custom_ca_bundle.pem"``` \

## Persistent setting (recommended for regular use):
**Linux/macOS: **\
Add the export line to your shell's profile file (e.g., ```~/.bashrc```, ```~/.zshrc```, ```~/.profile```). \
**Windows:** \
Set it as a system or user environment variable through the System Properties GUI (Environment Variables button).
## Test Your Azure CLI Connection

After setting the environment variable, restart your terminal or command prompt (if you set it persistently) and try an Azure CLI command:

```az account show```
