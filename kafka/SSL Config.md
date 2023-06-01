# How to configure the Kafka Server with the SSL Certificates

## 1- Generate CA (Certificate Authority) files:

```
openssl req -new -x509 -keyout ca-key.pem -out ca-cert.pem -days 3650 -nodes
```

## 2- Generate server key and certificate with SANs:

```
openssl req -newkey rsa:2048 -nodes -keyout server-key.pem -out server-csr.pem
```
 
## 3- 
```

openssl x509 -req -in server-csr.pem -CA ca-cert.pem -CAkey ca-key.pem -CAcreateserial -out server-cert.pem -days 3650 -extfile server.ext
```

### Server.ext = txtfile with <subjectAltName = DNS:localhost,IP:127.0.0.1> inside it 

## 4- Generate client key and certificate with SANs:
```
openssl req -newkey rsa:2048 -nodes -keyout client-key.pem -out client-csr.pem
```
```
openssl x509 -req -in client-csr.pem -CA ca-cert.pem -CAkey ca-key.pem -CAcreateserial -out client-cert.pem -days 3650 -extfile client.ext
```
### client.ext = txtfile with <subjectAltName = DNS:localhost,IP:127.0.0.1> inside it 

## Convert the server and client certificates to PKCS12 format (optional, for Java-based applications):

## 5- 
```
openssl pkcs12 -export -in server-cert.pem -inkey server-key.pem -out server.keystore.p12 -name server -CAfile ca-cert.pem -caname root
```
```
openssl pkcs12 -export -in client-cert.pem -inkey client-key.pem -out client.keystore.p12 -name client -CAfile ca-cert.pem -caname root
```

## Convert the server and client PKCS12 files to JKS format (Java KeyStore):
```
keytool -importkeystore -srckeystore server.keystore.p12 -srcstoretype PKCS12 -destkeystore server.keystore.jks -deststoretype JKS
```
```
keytool -importkeystore -srckeystore client.keystore.p12 -srcstoretype PKCS12 -destkeystore client.keystore.jks -deststoretype JKS
```
## Import the Certificate to the Stores
```
keytool -import -file ca-cert.pem -alias root -keystore server.truststore.jks
keytool -import -file ca-cert.pem -alias root -keystore client.truststore.jks
```

```
 openssl x509 -in ca-cert.pem -out ca-cert.crt
 openssl x509 -in client-cert.pem -out client-cert.crt
 openssl rsa -in client-key.pem -out client-key.key
```

## Edit the properties files:

# server.properties

```
listeners=PLAINTEXT://localhost:9092,SSL://localhost:9093


security.inter.broker.protocol=SSL
ssl.keystore.location= C:/kafka/security2/server.keystore.jks
ssl.keystore.keypassword=123456
ssl.keystore.password=123456
ssl.key.password=123456
ssl.truststore.location= C:/kafka/security2/server.truststore.jks
ssl.truststore.password=123456
ssl.client.auth=required
ssl.protocol=TLSv1.2
```


# client.properties
If the file do not exist create it
```
bootstrap.servers=localhost:9093
security.protocol=SSL
ssl.keystore.location= C:/kafka/security2/client.keystore.jks
ssl.keystore.keypassword=123456
ssl.keystore.password=123456
ssl.key.password=123456
ssl.truststore.location= C:/kafka/security2/client.truststore.jks
ssl.truststore.password=123456
```
```
.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

.\bin\windows\kafka-server-start.bat config\server.properties

.\bin\windows\kafka-console-consumer.bat --topic quickstart-events --bootstrap-server localhost:9093 --consumer.config config/client.properties
```

