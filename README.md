# CA Trust Automation
This repo provides examples for different languages that use Red Hat provided S2I images to eliminate the need for custom built extension images to inject CA trust stores to trust endpoints in an enterprise environment.

## Prerequisites
* helm >= 3
* [cert-utils-operator](https://github.com/redhat-cop/cert-utils-operator)
* [resource-locker]() - temporary until [#52](https://github.com/redhat-cop/cert-utils-operator/issues/52) is resolved

## Samples

### Java
An example deployment and generic services that demonstrate how to configure and use existing Java based applications to have a generated truststore tha comes from the OpenShift network operator injector.