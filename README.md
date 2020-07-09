# CA Trust Automation
This repo provides examples for different languages that use Red Hat provided S2I images to eliminate the need for custom built extension images to inject CA trust stores to trust endpoints in an enterprise environment.

## How it Works
The examples use a combination of projects to accomplish the end goal of the OpenShift platform to inject the CA trusts that are configured by the administrators of OpenShift.  This is similar to how when running VMs a Linux Admin would provide an image with the trust stores as part of a build and maintain and update them as the enterprise changes.  In order to get the trusted CA bundle from the platform the example utilizes the OpenShift cluster-network-operator to inject the bundle into a configmap.  Then the example demonstrates either using the podpreset admission controller to automatically add the volume mounts for the certificates, or directly add the volumemounts to the deploymentconfigs.  In the case of a Java application we also utilize the cert-utils-operator to convert the PEM ca bundle to a JKS cacerts trust store, and attach it in the same manner as a normal PEM bundle.  The key is that this method overrides the location of the generated certs that exist in the RHEL based pki directories.

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