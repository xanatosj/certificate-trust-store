# AWS CLI

Configuring the AWS CLI to Trust the Custom CA

### Method 1 - Using the ca_bundle setting in the AWS CLI config file
This is often the cleanest and most persistent method.

Locate your AWS CLI config directory:

* Linux/macOS: ```~/.aws/```
* Windows: ```%USERPROFILE%\.aws\```
  
Create or edit the config file: Inside the .aws directory, you'll find a file named config. Open it with a text editor.

Add the ca_bundle setting: Under the relevant profile (e.g., [default] or a named profile), add the ca_bundle line pointing to your PEM-encoded CA certificate bundle file.

Example ```~/.aws/config``` file:
```
[default]
region = us-east-1
output = json
ca_bundle = /path/to/your/custom_ca_bundle.pem

[profile my-dev-profile]
region = us-west-2
output = text
ca_bundle = C:\certs\corporate_root_ca.pem
```
_Replace /path/to/your/custom_ca_bundle.pem or C:\certs\corporate_root_ca.pem with the actual path to your certificate bundle file._

### Method 2 - Using the AWS_CA_BUNDLE environment variable
This method is useful for temporary configurations or when you want to apply the setting for a specific session or script.

Set the environment variable: 
* Linux/macOS: \
```export AWS_CA_BUNDLE="/path/to/your/custom_ca_bundle.pem"```
* Windows (Command Prompt): \
```set AWS_CA_BUNDLE="C:\path\to\your\custom_ca_bundle.pem"```
* Windows (PowerShell): \
```$env:AWS_CA_BUNDLE="C:\path\to\your\custom_ca_bundle.pem"```

_Note: For Windows, ensure the path uses backslashes and is enclosed in double quotes if it contains spaces._

## Test Command
After configuring, run a simple AWS CLI command to verify that it can now communicate successfully without SSL errors.
> ```aws s3 ls```
