# PHP

There are a few ways to achieve this, depending on which part of PHP is making the request and your environment setup.

## Method A: Configure php.ini (Recommended for Server-Side PHP)

Locate your php.ini file:
Common locations: /etc/php/<version>/apache2/php.ini, /etc/php/<version>/fpm/php.ini, /etc/php/<version>/cli/php.ini, or similar

Add/Edit curl.cainfo and openssl.cafile: Open your php.ini file and find (or add) these directives:

* For PHP's stream wrappers (file_get_contents with https://) and other OpenSSL-related functions
```
openssl.cafile = "/path/to/your/custom_ca_bundle.pem"
```

* For the cURL extension (used by many HTTP client libraries like Guzzle)
```
curl.cainfo = "/path/to/your/custom_ca_bundle.pem"
```
_Replace /path/to/your/custom_ca_bundle.pem with the actual full path to your PEM-encoded certificate bundle file._

## Method B: Specify CA File in PHP Stream Context (Per-Request)
If you're using file_get_contents or other stream functions, you can specify the CA bundle directly in the stream context options. This is useful if you don't want to change php.ini globally.

```
<?php
$context = stream_context_create([
    'ssl' => [
        'cafile' => '/path/to/your/custom_ca_bundle.pem',
        'verify_peer' => true,
        'verify_peer_name' => true,
    ],
]);

$response = file_get_contents('https://your-target-url.com/', false, $context);

if ($response === false) {
    echo "Error fetching URL.\n";
} else {
    echo $response;
}
?>
```

## Testing
Log into the server where PHP is running and try to curl the target URL using your custom CA bundle to verify network connectivity and certificate chain from the server's perspective:\
```curl -v --cacert /path/to/your/custom_ca_bundle.pem https://your-target-url.com/```
