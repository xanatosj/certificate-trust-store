# wget

To add the custom Root CA certificate for GNU Wget, use the ```--ca-certificate=FILE``` command to trust the Root CA certificate bundle. 

```wget --ca-certificate ca-cert-bundle.pem https://www.google.com```

You can also set the environment variable using this command:

```echo "ca_certificate=ca-cert-bundle.pem" >> $HOME/.wgetrc```
