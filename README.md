# AWS Distro for OpenTelemetry Ruby

## Introduction

AWS Distro for OpenTelemetry Ruby (ADOT Ruby) refers to a distribution of [OpenTelemetry Ruby](https://github.com/open-telemetry/opentelemetry-ruby) that has been packaged with components necessary to make it compatible with the AWS X-Ray service. This way, traces generated by OpenTelemetry Ruby can be queried in the [AWS X-Ray console](https://console.aws.amazon.com/xray/home) where users can see information such as the duration, method invoked, status codes, and more.

This repository contains sample applications that are instrumented with ADOT Ruby. GitHub workflows on this repository continuously validate the integration experience of these sample apps with the AWS X-Ray backend using the [ADOT Test Framework](https://github.com/aws-observability/aws-otel-test-framework/tree/terraform). Use this repo to raise issues regarding ADOT Ruby integration or to discuss adding enhancements that cannot be covered by OpenTelemetry Ruby.

This repo is regularly monitored by the AWS Observability team.

## How it works

OpenTelemetry is an open source project that give users better observability into their system. OpenTelemetry collects distributed traces and metrics from several popular packages your application is already using and exports the information to backends. As a backend, AWS X-Ray makes it easy to visualize and query traces in a user-friendly console packed with features to help users understand what happened during traced calls. Learn more about AWS X-Ray in the [developer guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html).

When OpenTelemetry exports traces to the AWS X-Ray Console, the traces include parameters used in the call, results, exceptions, and more in the trace attributes. Read more about standardized attributes on the OpenTelemetry Specification [Semantic Conventions for traces](https://github.com/open-telemetry/opentelemetry-specification/tree/main/specification/trace/semantic_conventions).

To fully take advantage of the features of ADOT Ruby with AWS X-Ray, **we recommend you use both the X-Ray IDs Generator and the X-Ray Propagator when configuring the OpenTelemetry Ruby SDK**. The X-Ray IDs Generator makes sure Trace IDs are in the format AWS X-Ray expects, and the X-Ray Propagator adds a [X-Ray Tracing Header](https://docs.aws.amazon.com/xray/latest/devguide/xray-concepts.html#xray-concepts-traces) to outgoing requests so that the same context is propagated across different services and you get a connected view of all the traces in the X-Ray console.

To send traces to AWS X-Ray, use the [ADOT Collector](https://github.com/aws-observability/aws-otel-collector). The ADOT Collector includes packages from the [OpenTelemetry Collector](https://github.com/open-telemetry/opentelemetry-collector) to allow exporting to AWS X-Ray. ADOT Ruby is configured to export traces to the ADOT Collector and the collector uses its provided permissions and configuration to send those traces to AWS X-Ray.

## Getting Started

Check out our public documentation for [tracing applications with ADOT Ruby](https://aws-otel.github.io/docs/getting-started/ruby-sdk/trace-manual-instr) to help you get started.

### Sample Application - Manual instrumentation

See [a sample app manually instrumented with ADOT Ruby](sample-apps/manual-instrumentation/ruby-on-rails/README.md) that you can run yourself to understand the necessary setup for ADOT Ruby.

## Requirements

Ruby 2.5+ is required to use OpenTelemetry Ruby. Check your currently installed Ruby version using `ruby -v`.

## Useful Links

Find out more about AWS X-Ray Tracing with Opentelemetry Ruby at the
following links.

- [OpenTelemetry Ruby GitHub](https://github.com/open-telemetry/opentelemetry-ruby)
- [ADOT Ruby X-Ray Propagator Package](https://github.com/open-telemetry/opentelemetry-ruby/tree/main/propagator/xray#opentelemetry-propagator-xray)
- [AWS Distro for OpenTelemetry](https://aws-otel.github.io/)

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This project is licensed under the Apache-2.0 License.
