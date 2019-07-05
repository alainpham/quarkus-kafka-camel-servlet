# Wiring together camel-core camel-servlet and smallrye-reactive-messaging-kafka within Quarkus

This project show how to :
 
- Configure Camel Servlet extension to Undertow http endpoint provided by Quarkus
- Wire a SmallRye emitter to the camel-context for Camel to send message to kafka
- Wire a Camel producer template to a SmallRye incoming annotated method for Camel to receive messages from Kafka


More details here Link to blog article to come


Compile natively

```
mvn package -Pnative
```

Create container image

```
docker build -f src/main/docker/Dockerfile.native -t quarkus/quarkus-kafka-camel-servlet .
```

Create adjust docker compose image with customized environment props

```
cat src/main/resources/application.properties | awk -F= '{gsub("\\.|-","_",$1) ;print "export " toupper($1)  "=" $2 }'
```

To run everything (Kafka + Project) locally :

```
docker-compose up
```