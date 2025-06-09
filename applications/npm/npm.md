# Configure npm to Trust the Custom CA

**You have a few ways to do this, ranging from the npm configuration to environment variables:**

## Method A: Using npm config set cafile (Recommended)

This is the most direct way to tell npm about your custom CA certificate.

```npm config set cafile /path/to/your/custom_ca_bundle.pem ```
* Replace ```/path/to/your/custom_ca_bundle.pem``` with the actual full path to your PEM-encoded certificate bundle file.

* This command modifies your global ```.npmrc``` file (usually located at ```~/.npmrc on Linux/macOS``` or ```C:\Users\<YourUser>\.npmrc``` on Windows) to include the cafile setting.
* Important Note: Setting cafile makes npm only trust the certificates in that file. If you need to trust the standard public CAs and your custom CA, you'll need to create a bundle that includes both. Often, the default cacerts.pem from Node.js or certifi can be combined with your custom CA. A more flexible approach for extending the trust is using ```NODE_EXTRA_CA_CERTS``` (Method B).

## Method B: Using the NODE_EXTRA_CA_CERTS Environment Variable

This method is often preferred for more complex scenarios or when you want to extend Node.js's default trusted CAs rather than replacing them entirely. This applies to npm because npm runs on Node.js.

Set the environment variable: \
**Linux/macOS (for current session):**  \
```export NODE_EXTRA_CA_CERTS="/path/to/your/custom_ca_bundle.pem" ``` \
**Windows (Command Prompt - for current session):** \
```set NODE_EXTRA_CA_CERTS="C:\path\to\your\custom_ca_bundle.pem"``` \
**Windows (PowerShell - for current session):** \
```$env:NODE_EXTRA_CA_CERTS="C:\path\to\your\custom_ca_bundle.pem"``` 

Persistent setting (recommended for regular use):\
**Linux/macOS:**  \
Add the export line to your shell's profile file (e.g., ```~/.bashrc```, ```~/.zshrc```, ```~/.profile```). \
**Windows:**  Set it as a system or user environment variable through the System Properties GUI (Environment Variables button). \
**Key Advantage:**  ```NODE_EXTRA_CA_CERTS``` tells Node.js to load your specified certificate(s) in addition to its default set of trusted CAs, which is often what you want. 

## Test Your npm Connection

After configuring, try a simple npm command: \
``` npm install ``` \
or  \
```npm update``` \
If the custom certificate is correctly trusted and proxy settings are accurate, npm should now be able to fetch packages without SSL errors.
