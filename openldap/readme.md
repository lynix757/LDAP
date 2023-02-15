# OpenLDAP with phpldapadmin

mkdir certs
cd certs

https://www.sslshopper.com/article-most-common-openssl-commands.html

################################# RootCA #################################
### Generate Key *mycompany
openssl genrsa -des3 -out rootCA.key 2048

### Generate Certificate
openssl req -subj '/C=TH/OU=IT/CN=MYCOMPANY' -x509 -new -nodes -key rootCA.key -sha256 -days 3560 -out rootCA.pem

### Check Certificate info
openssl x509 -in rootCA.pem -text -noout


################################# SSL Cert #################################
### Generate Key 
openssl genrsa -out openldap.key 2048

### Generate CSR
openssl req -subj '/C=TH/OU=IT/CN=openldap.mycompany' -new -key openldap.key -out openldap.csr

### Check CSR info
openssl req -in openldap.csr -text -noout

### Sign Certificate with rootCA
openssl x509 -req -in openldap.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out openldap.crt -days 1825 -sha256




