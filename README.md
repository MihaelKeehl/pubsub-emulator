# Based on Google SDK image example

[google/cloud-sdk](https://hub.docker.com/r/google/cloud-sdk/dockerfile)

# Google Cloud PubSub Emulator

[Google Cloud PubSub Emulator](https://cloud.google.com/sdk/gcloud/reference/beta/emulators/pubsub/) unofficial container image for testing.

## Application variables

Please set these variables in the application to connect to emulator:

- `PUBSUB_EMULATOR_HOST`: The listen address used by the emulator.
- `PUBSUB_PROJECT_ID`: The ID of the Google Cloud project used by the emulator.

## Creating a PubSub emulator

Data can be mounted on "/data"

[Docker Compose](https://docs.docker.com/compose).

```YAML
version: "2"

services:
  datastore:
    image: MihaelKeehl/pubsub-emulator:latest
    environment:
      - DATASTORE_PROJECT_ID=project-test
    ports:
      - "8538:8538"
```

Kubernetes:

```kubectl run pubsub-emulator --image=MihaelKeehl/pubsub-emulator:latest --restart=Always --port=8538
  kubectl expose deployment pubsub-emulator --port 8538 --target-port 8538 --name pubsub-emulator --type ClusterIP
kubectl wait --for=condition=Ready pod -l run=pubsub-emulator --timeout 1m```
