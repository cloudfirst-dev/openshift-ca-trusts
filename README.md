# CA Trust Automation
This repo provides examples for different languages that use Red Hat provided S2I images to eliminate the need for custom built extension images to inject CA trust stores to trust endpoints in an enterprise environment.

## Prerequisites
* helm >= 3
* [cert-utils-operator](https://github.com/redhat-cop/cert-utils-operator)

### Podpreset

This example also demonstrates using a webhook to mutate the pods to include the volume mounts and simplify the developer requirements to consume the certificates.  This can be turned off in all the examples by setting use_preset to false in any of the example languages.

#### Deploy

To deploy the pod preset this repo includes a convenience helm chart and expects to be deployed in the podpreset-webhook namespace.  To deploy you must have cluster admin privileges.

```
oc new-project podpreset-webhook
helm install podpreset podpreset/helm
```

## Samples

### Java
An example deployment and generic services that demonstrate how to configure and use existing Java based applications to have a generated truststore tha comes from the OpenShift network operator injector.  This method does require the cert-utls-operator to perform the conversion from a pem format to a jks format.

### Dotnet
An example deployment and generic services that demonstrate how to configure a dotnet core application to consume the truststores.  This method does not require the cert-utils-operator.