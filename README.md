# cert
create self sign cert from private ca

```bash

# Path to the Organisation Unit (OU)
SUBJECT_OU="/C=FR/ST=NANTES/L=NANTES/O=MyOrga/OU=IT"

# DNS list 
SUBJECT_ALT_NAME="DNS:example.com, DNS:www.example.com"

# Create a CA key
openssl genrsa -out ca.key 4096

# Create a CA certificate (from the CA key)
openssl req -new -x509 -days 365 -key ca.key -subj "$SUBJECT_OU/CN=MyOrga Root CA" -out ca.crt

# Create a server key and a Certificate Signing Request (CSR) for this server key
openssl req -newkey rsa:4096 -nodes -keyout server.key -subj "$SUBJECT_OU/CN=MyCert" -out server.csr

# Create a certificate (from the key and the CSR) with the DNS aliases
openssl x509 -req -extfile <(printf "subjectAltName=$SUBJECT_ALT_NAME") -days 365 -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server.crt

# Display the certificat
openssl x509 -in server.crt -text

```

