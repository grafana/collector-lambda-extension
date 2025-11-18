# Collector Lambda Extension

This repository contains a custom distribution of the [opentelemetry-lambda](https://github.com/open-telemetry/opentelemetry-lambda/tree/main/collector) collector layer.

It is built using the upstream repository with a different [default configuration file](./collector/config.yaml).

## Usage

### Add the Extension Layer
Add the extension layer ARN to your Lambda function. You can find the correct ARN for your region on the [releases page](https://github.com/grafana/collector-lambda-extension/releases).

### Add the Instrumentation Layer
Add the language specific [instrumentation layer](https://opentelemetry.io/docs/platforms/faas/lambda-auto-instrument/#add-the-arn-of-instrumentation-lambda-layer) from the [releases](https://github.com/open-telemetry/opentelemetry-lambda/releases) page.

### Set Environment Variables
Set the following environment variables to the values provided by your [Grafana Cloud Stack](https://grafana.com):

| Name                          | Value                                                                                                                                  |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `GRAFANA_CLOUD_INSTANCE_ID`   | Your Grafana Cloud instance ID. Example: `650111`                                                                                      |
| `GRAFANA_CLOUD_OTLP_ENDPOINT` | Endpoint for sending OTLP signals. Example: `https://otlp-gateway-prod-eu-west-2.grafana.net/otlp`                                     |
| `GRAFANA_CLOUD_API_KEY_ARN`   | An AWS Secrets Manager ARN for the Grafana Cloud Token. Example `arn:aws:secretsmanager:us-west-2:...:secret:some-secret#GCLOUD_TOKEN` |


You can find your instance ID and OTLP endpoint in the [Grafana Cloud Console](https://grafana.com/profile/org).  
Go to the details of the stack you want to send data to and then choose the OpenTelemetry card.  
On this page, you'll find the OTLP endpoint as well as the instance ID.  

When referencing a secret from the AWS Secret Manager, you'll also need to ensure that the lambda role has the `secretsmanager:GetSecretValue` permission.  
Alternatively, you can use the `GRAFANA_CLOUD_API_KEY` environment variable to specificy the token directly but this isn't recommended and should only be used for testing.   

[Configure](https://opentelemetry.io/docs/platforms/faas/lambda-auto-instrument/#configure-your-sdk-exporters) your SDK Exporters with the variables specific to your language. 