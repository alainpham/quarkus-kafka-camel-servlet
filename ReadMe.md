# Wiring together camel-core camel-servlet and smallrye-reactive-messaging-kafka within Quarkus

This project show how to :
 
- Configure Camel Servlet extension to Undertow http endpoint provided by Quarkus
- Wire a SmallRye emitter to the camel-context for Camel to send message to kafka
- Wire a Camel producer template to a SmallRye incoming annotated method for Camel to receive messages from Kafka


More details here Link to blog article.


Compile natively

```
mvn package -Pnative
```

Create container image

```
docker build -f src/main/docker/Dockerfile.native -t quarkus/quarkus-kafka-camel-servlet .
```

Create adjust docker compose image with customized environment props. The following command will help you convert prop files into environment variable standard.

```
cat src/main/resources/application.properties | awk -F= '{gsub("\\.|-","_",$1) ;print "export " toupper($1)  "=" $2 }'
```

To run everything (Kafka + Project) locally :

```
docker-compose up
```

You can get the container image here

https://hub.docker.com/r/alainpham/quarkus-kafka-camel-servlet

To test it 

```
curl http://localhost:8080/camel/send  -X POST -H "Content-Type: text/plain"  -d 'Hello there!!'
```
