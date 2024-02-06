# Kubernetes APIM Deployment Single Node Deployment 

This repository is designed to help you learn the basics of Kubernetes (K8s) resources, with a focus on deploying an API Manager (APIM) single-node instance into a Kubernetes cluster.

<img width="860" alt="apimk8" src="https://github.com/cbabey/kubernetes-apim-resources/assets/42814210/5a263132-e3bd-43fc-b2f4-0aecefd0bcf6">

## Prerequisites

Before deploying the K8s resources in this repository, ensure you have completed the following prerequisites:

1. Set up a Kubernetes cluster.
2. Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git),[Kubernetes client](https://kubernetes.io/docs/tasks/tools/install-kubectl/) in order to run the steps provided in the
  following quick start guide.
2. Install [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/deploy/).
3. Clone [this github repository](https://github.com/cbabey/kubernetes-apim-resources).

##  Setup and Apply K8s Resources

Follow these steps to deploy APIM in your Kubernetes cluster:

1. Create a namespace named `apimdev`:

   ```bash
   kubectl create namespace apimdev
   ```

2. Navigate to the directory `kubernetes-apim-resources/simple/am-single` in the cloned repository.

3. Execute the following command to apply the K8s resources:

   ```bash
   kubectl apply -f .
   ```
## Validating the Deployment

Ensure the successful deployment of APIM in your Kubernetes cluster by following these steps:

1. **Check Pod Status:**
   Verify that the pods related to the APIM deployment are running successfully.

   ```bash
   kubectl get pods -n apimdev
   ```

2. **Check Services:**
   Verify that the necessary services are running and have ClusterIP or External IP assigned.

   ```bash
   kubectl get services -n apimdev
   ```

3. **Verify Ingress Resources:**
   Ensure that the Ingress resources are correctly configured.

   ```bash
   kubectl get ing -n apimdev
   ```


## Accessing the APIM Server

After successful deployment, access the APIM server using the following steps:

1. Obtain the external IP address of the Ingress resources:

   ```bash
   kubectl get ing -n apimdev
   ```

   Example output:

   ```plaintext
   NAME                                    CLASS    HOSTS                     ADDRESS       PORTS     AGE
   wso2am-single-node-am-servlet-ingress   <none>   dev.am.wso2.com           172.20.10.4   80, 443   29m
   wso2am-single-node-am-gateway-ingress   <none>   dev.gateway.am.wso2.com   172.20.10.4   80, 443   29m
   ```

2. Add DNS mappings to your `/etc/hosts` file:

   ```plaintext
   172.20.10.4  dev.am.wso2.com dev.gateway.am.wso2.com
   ```

   Replace `172.20.10.4` with the actual external IP obtained in the previous step.
