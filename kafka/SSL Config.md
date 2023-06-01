#How to configure the Kafka Server with the SSL Certificates

##Generate CA (Certificate Authority) files:

openssl req -new -x509 -keyout ca-key.pem -out ca-cert.pem -days 3650 -nodes
