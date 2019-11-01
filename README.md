# Pihole Exporter Helm Chart

TL;DR;

```helm install -name pihole-exporter --namespace pihole ./```

## Introduction

This chart deploys the pihole-exporter by eko - https://github.com/eko/pihole-exporter to a kubernetes cluster.

## Notes
I have not set a default configuration, please modify the values.yaml file with your correct config settings.

## Configuration

| Parameter                      | Description                            | Default            |
| ------------------------------ |:--------------------------------------:| ------------------:|
| service.port                   | Port for the kubernetes service        | 9617               |
| extraEnvVars.INTERVAL          | How often to poll pihole stats         | 10s                |
| extraEnvVars.PIHOLE_HOSTNAME   | Pihole Hostname                        | None               |
| extraEnvVars.PIHOLE_PASSWORD   | Pihole admin user password             | None               |
| extraEnvVars.PORT              | Change default webserver port for app  | 9617               |
