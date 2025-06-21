Guides for Ingress and TLS:

https://docs.digitalocean.com/products/kubernetes/getting-started/operational-readiness/enable-https/


### Install Cert Manager
  Currently:
    - DigitalOcean Marketplace in the web UI.
  Preferred:
    - Create with the Terraform resource.
`install cert manager`

### Install Nginx
`helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx`
`helm repo update`
`helm install ingress-nginx ingress-nginx/ingress-nginx --set controller.publishService.enabled=true`
`kubectl --namespace default get services -o wide -w nginx-ingress-ingress-nginx-controller`
add   lb ip to A records

`kubectl get ingress`
`kubectl get certificates`



```
You can watch the status by running 'kubectl get service --namespace default nginx-ingress-ingress-nginx-controller --output wide --watch'

An example Ingress that makes use of the controller:
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: example
    namespace: foo
  spec:
    ingressClassName: nginx
    rules:
      - host: www.example.com
        http:
          paths:
            - pathType: Prefix
              backend:
                service:
                  name: exampleService
                  port:
                    number: 80
              path: /
    # This section is only required if TLS is to be enabled for the Ingress
    tls:
      - hosts:
        - www.example.com
        secretName: example-tls

If TLS is enabled for the Ingress, a Secret containing the certificate and key must also be provided:

  apiVersion: v1
  kind: Secret
  metadata:
    name: example-tls
    namespace: foo
  data:
    tls.crt: <base64 encoded cert>
    tls.key: <base64 encoded key>
  type: kubernetes.io/tls
helm```