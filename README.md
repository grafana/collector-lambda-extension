# Collector Lambda Extension

This repository contains a custom distribution of the [opentelemetry-lambda](https://github.com/open-telemetry/opentelemetry-lambda/tree/main/collector) collector layer.

It is built using the upstream repository with a different [default configuration file](config.yaml).

## Usage

Add the extension layer ARN to your Lambda function. You can find the correct ARN for your region on the [releases page](/releases).
Set the following environment variables to the values provided by your [Grafana Cloud Stack](https://grafana.com):

| Name                          | Value                                                                                                                                  |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `GRAFANA_CLOUD_INSTANCE_ID`   | Your Grafana Cloud instance ID. Example: `650111`                                                                                      |
| `GRAFANA_CLOUD_OTLP_ENDPOINT` | Endpoint for sending OTLP signals. Example: `https://otlp-gateway-prod-eu-west-2.grafana.net/otlp`                                     |
| `GRAFANA_CLOUD_API_KEY`       | Your Grafana Cloud Token. Needs write premissions. Example: `glc...`                                                                   |
| `GRAFANA_CLOUD_API_KEY_ARN`   | An AWS Secrets Manager ARN for the Grafana Cloud Token. Example `arn:aws:secretsmanager:us-west-2:...:secret:some-secret#GCLOUD_TOKEN` |

Only one of `GRAFANA_CLOUD_API_KEY` and `GRAFANA_CLOUD_API_KEY_ARN` needs to be defined.
Prefer using the Secrets Manager ARN as Lambda environment variables are not secret.
