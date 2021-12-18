# ycit021-myapp

## Application information
The application has been built with this [repository](https://github.com/NicolasHostert/nuxt-realworld).

The Docker image is stored [there](https://hub.docker.com/layers/nhostert/myapp/v3/images/sha256-d1bd0de89614a2e61a375ad25bcecf1eb2aa96d60a3b51e1340b0521c628c1a2?context=explore).

## Installation procedure

### Local dev machine

    helm install myapp . --values values-local.yaml

Then run these commands to get the info of your service:

    export NODE_PORT=$(kubectl get --namespace {{ .Release.Namespace }} -o jsonpath="{.spec.ports[0].nodePort}" services {{ include "myapp.fullname" . }})
    export NODE_IP=$(kubectl get nodes --namespace {{ .Release.Namespace }} -o jsonpath="{.items[0].status.addresses[0].address}")
    echo http://$NODE_IP:81

### On the cloud

    helm install myapp . --values values-cloud.yaml
Then run these commands to get the info of your service:

    export SERVICE_IP=$(kubectl get svc --namespace default ycit021-myapp --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")
    echo http://$SERVICE_IP:80
