To create a local root certificate for a HTTPS connection to localhost

```bash
#Create root key
openssl genrsa -des3 -out rootCA.key 2048
#Create root cert
openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.pem
#Add root cert
sudo security add-trusted-cert -d -r trustRoot -k /Library/Keychains/System.keychain rootCA.pem
```

Create a server configuration `server.csr.cnf`

```bash
echo '[req]' > server.csr.cnf
echo 'default_bits = 2048' >> server.csr.cnf
echo 'prompt = no' >> server.csr.cnf
echo 'default_md = sha256' >> server.csr.cnf
echo 'distinguished_name = dn' >> server.csr.cnf
echo ' ' >> server.csr.cnf
echo '[dn]' >> server.csr.cnf
echo 'C=US' >> server.csr.cnf
echo 'ST=RandomState' >> server.csr.cnf
echo 'L=RandomCity' >> server.csr.cnf
echo 'O=RandomOrganization' >> server.csr.cnf
echo 'OU=RandomOrganizationUnit' >> server.csr.cnf
echo 'emailAddress=hello@example.com' >> server.csr.cnf
echo 'CN = localhost' >> server.csr.cnf
```

Create `v3.ext`

```bash
echo 'authorityKeyIdentifier=keyid,issuer' > v3.ext
echo 'basicConstraints=CA:FALSE' >> v3.ext
echo 'keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment' >> v3.ext
echo 'subjectAltName = @alt_names' >> v3.ext
echo ' ' >> v3.ext
echo '[alt_names]' >> v3.ext
echo 'DNS.1 = localhost' >> v3.ext
```

Generate `server.csr` and `server.key`

```bash
openssl req -new -sha256 -nodes -out server.csr -newkey rsa:2048 -keyout server.key -config <( cat server.csr.cnf )
```



Generate `server.crt`

```bash
openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out server.crt -days 500 -sha256 -extfile v3.ext
```



