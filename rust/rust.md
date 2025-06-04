# Rust
On Linux-based systems, there is a built-in system command to add self-signed certificates (Root CA) to the trust store.

Place root certificate(s) in the following directory\
```/usr/local/share/ca-certificates/```

Update the CA store using the following command:\
```sudo update-ca-certificates```
