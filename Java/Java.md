# Java

> keytool -import -trustcacerts -alias <your_alias> -file <path_to_your_certificate_file> -keystore <path_to_cacerts_file> -storepass changeit

## Step by Step

### Locate your CA Certs files
The cacerts file is usually located in your Java installation directory:
> JDK: $JAVA_HOME/lib/security/cacerts

> JRE: $JAVA_HOME/jre/lib/security/cacerts

You can also find the java.home property in your Java application to confirm the JRE path.


### Backup your cacerts file
Create a backup copy of your cacerts file. This allows you to revert if something goes wrong.

> cp $JAVA_HOME/lib/security/cacerts $JAVA_HOME/lib/security/cacerts_backup

### Import the certificate using keytool

Open your command prompt or terminal and navigate to the bin directory of your Java installation (e.g., $JAVA_HOME/bin). Then, use the keytool command to import the certificate:
> keytool -import -trustcacerts -alias <your_alias> -file <path_to_your_certificate_file> -keystore <path_to_cacerts_file> -storepass changeit

Explanation of parameters:

**-import**: Specifies that you want to import a certificate. \
**-trustcacerts**: Indicates that the certificate should be added to the trust store. \
**-alias <your_alias>**: A unique name you assign to the certificate in the keystore. Choose something descriptive (e.g., myproxyca, companyroot). \
**-file <path_to_your_certificate_file>**: The full path to the certificate file you want to import (e.g., C:\temp\myCert.cer or /home/user/myCert.pem). \
**-keystore <path_to_cacerts_file>**: The full path to your cacerts file. \
**-storepass changeit**: The password for the keystore. The default password for cacerts is changeit. 

### Verity the Import

You can list the contents of the cacerts file to confirm that your certificate has been imported successfully:
> keytool -list -keystore <path_to_cacerts_file> -storepass changeit -alias <your_alias>

### Restart your Java Application

After importing the certificate, you must restart any running Java applications that need to trust this new certificate. Java loads the cacerts file at startup
