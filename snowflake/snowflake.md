# Snowflake ODBC Connections

The Snowflake ODBC driver relies on system-level or driver-specific configuration to trust custom CAs.  For scenerios where it is not configured to trust the system custom CAs, you may need to use the ```CABundleFile``` configuration parameter 

## Using CABundleFile Parameter:

**Windows:** \
Configuration parameters are set in the Windows registry using regedit and the following registry path \
```[HKEY_LOCAL_MACHINE\SOFTWARE\Snowflake\Driver]```

**macOS or Linux**\
Configuration parameters are set in the configuration file ```simba.snowflake.ini``` 

## Configuration Parameter

```CABundleFile``` \
Set the location of the Certificate Authority (CA) bundle file. Must reference a file that includes a valid list of CA certificates.

* Linux, the RPM and DEB installers automatically copy the file and set this parameter.
* Mac, the PKG installer copies the file and sets this parameter.
* Windows, the MSI installer copies the file and sets this parameter.

Always refer to the official Snowflake ODBC Driver documentation for the most precise and up-to-date [connection parameters](https://docs.snowflake.com/en/developer-guide/odbc/odbc-parameters#label-odbc-connection-parameters:~:text=Configuration%20parameters-,CABundleFile,-Set%20the%20location)
