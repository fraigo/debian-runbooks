To create a local root certificate for a HTTPS connection to localhost

```bash
#Create root key
openssl genrsa -des3 -out rootCA.key 2048
#Create root cert
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem
#Add root cert
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain rootCA.pem
```

