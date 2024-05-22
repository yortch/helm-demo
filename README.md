# HELM Chart demo

To install helm chart run the following commands (assumes you are logged into your kubernetes cluster):

1. Create namespace
    ```
    NAMESPACE=helm-demo
    kubectl create namespace helm-demo
    ```
1. Install helm chart:
    ```
    helm upgrade -i demo-app demo-chart -n $NAMESPACE
    ```
1. Get IP of deployed service:
    ```
    export SERVICE_IP=$(kubectl get svc --namespace $NAMESPACE demo-app-demo-chart --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}")
    ```
1. Test service with curl command:
    ```
    curl http://$SERVICE_IP
    ```