# istio-kafka-kubernetes

Istio observability, kafka-message-bus backed communication, visible in kubernetes CRDs and observable in kaili

## Goals

The goals of this project are to combine the power of kafka, istio and kaili to provide maximum observability to a
cluster.

### Setting up Istio

- [ ] Deploy [istio](https://istio.io) to docker-kubernetes, documenting instructional resources used to get it working
      here
- [ ] Deploy [kiali](https://www.kiali.io), documenting anything required to get it working
- [ ] See the UI Kaili provides
- [ ] Deploy a fake microservices project and check the Kaili UI again (or something, not sure what e)

### Setting up Strimzi-Kafka

- [ ] Deploy [strimzi-kafka](https://strimzi.io/) CRD to docker-kubernetes, documenting instructional resources used to
      get it working here
- [ ] Deploy a strimzi-managed kafka instance

### Create a test job to validate future istio and Strimzi-Kafka both work

- [ ] Create a `test-kafka-istio-mongo` chart which does the following:
  - [ ] Deploys mongo instance
  - [ ] Deploys a kafka-rest service with virtual service entries
  - [ ] Deploys a mock kafka-producer-consumer, which copies messages sent by kafka-rest onto another topic
  - [ ] Deploys kafka-connect to mongo kafka-connector, which copies mirrored messages into a mongo instance
  - [ ] Deploys topic CRDs to create topics for all services
  - [ ] Deploys a rest-based kafka-producer which uses the virtual service kafka-rest provides to send messages
  - [ ] Checks data made it through the rest interface, through each of the kafka topics and into the mongo database

### Using istio to invisibly supply credentials to mongo

- [ ] Configure test job to set up mongo with non-default credentials, and to use ssl connections
- [ ] Set up istio to attach ssl-certs and user credentials to requests from microservices within the namespace to
      mongo, without further modifying the test-job.
- [ ] Rerun `test-kafka-istio-mongo` job to show data is entered into mongo with istio configuration

### <span style="color:red">HARD:</span> Using istio and kiali for kafka observability

- [ ] Configure istio to run requests to kafka topics through istio
- [ ] Istio to differentiate between requests to different topics
- [ ] Run test job
- [ ] Kaili must display messages flowing through different topics, from service to service

### Using istio with a secure kafka cluster

- [ ] Secure the strimzi-managed kafka instance with `ssl`
- [ ] Secure the strimzi-managed kafka instance with strimzi-managed `Users`
- [ ] Setup istio to supply these credentials to microservices running in a namespace at the network layer
- [ ] Rerun `test-kafka-istio-mongo` routing data from the kafka-producer, showing it still passes

### Using istio and kafka with a schema-registry

- [ ] Deploy a `schema-registry`
- [ ] Create a mock `schema` in the `schema-registry`
- [ ] Set up services to use the `schema-registry` schemas when using messages
- [ ] Rerun `test-kafka-istio-mongo` routing data from the kafka-producer, showing it still passes

### EVEN MORE

- [ ] configure Strimzi-Kafka Topics and Users ACL to work with an external kafka as well as an internal one
- [ ] configure istio to proxy external TCP services (may not be appropriate for this project specifically)
- [ ] schema-registry ACL

At this point, we'd have something set up for multitenancy.
