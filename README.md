# Pihole Exporter Helm Chart

TL;DR;

```
helm install -name pihole-exporter --namespace pihole ./
```

Using an auth token:
```
helm install \
  -name pihole-exporter \
  --namespace pihole \
  --set secret.secretEnvVars.PIHOLE_API_TOKEN=myPiHoleApiToken \
  ./
```

Using a password:
```
helm install \
  -name pihole-exporter \
  --namespace pihole \
  --set secret.secretEnvVars.PIHOLE_PASSWORD=myPiHolePassword \
  ./
```

Using an existing secret in the same namespace:
```
helm install \
  -name pihole-exporter \
  --namespace pihole \
  --set secret.generate=false \
  --set secret.existing.secretName=my-pi-hole-secret \
  ./
```

Setting the hostname with a password:
```
helm install \
  -name pihole-exporter \
  --namespace pihole \
  --set secretEnvVars.PIHOLE_PASSWORD=myPiHolePassword \
  --set extraEnvVars.PIHOLE_HOSTNAME=my.pihole.server \
  ./
```

## Introduction

This chart deploys the pihole-exporter by eko - https://github.com/eko/pihole-exporter to a kubernetes cluster.

## Configuration

> The default configuration is very rudimentary, please override values as required for your configuration.

To override the default you can either :
* Set the individual values as required as part if the helm command (i.e. `--set some.value=MY_VALUE`)
* Create your own `my-values.yaml` containing your custom values (i.e. `helm install -f my-values.yaml .`)
* (Least preferred) Modify the `values.yaml` file with your configuration.

| Parameter                            | Description                                                                                 |           Default |
|:-------------------------------------|:--------------------------------------------------------------------------------------------|------------------:|
| service.port                         | Port for the kubernetes service                                                             |              9617 |
| extraEnvVars.INTERVAL                | How often to poll pihole stats                                                              |               10s |
| extraEnvVars.PIHOLE_HOSTNAME         | Pihole Hostname                                                                             |              None |
| extraEnvVars.PORT                    | Change default webserver port for app                                                       |              9617 |
| secret.generate                      | Generate a new secret based on the `secretEnvVars` value/s                                  |              true |
| secret.secretEnvVars.PIHOLE_PASSWORD | Pihole admin user password                                                                  |              None |
| secret.secretEnvVars.PIHOLE_APITOKEN | Pihole api token                                                                            |              None |
| secret.existing.secretName           | The name of an existing secret containing the Pihole credentials                            | my-pi-hole-secret |
| secret.existing.piHoleCredentialType | The type of piHole credential in the secret, either 'PIHOLE_API_TOKEN' or 'PIHOLE_PASSWORD' |  PIHOLE_API_TOKEN |
| secret.existing.secretKey            | The key within the secret containing the piHole api token or password                       |  PIHOLE_API_TOKEN |
