# ycit021-myapp

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
