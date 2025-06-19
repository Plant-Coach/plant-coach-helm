# Plant Coach Helm
- *This customizable Helm Chart deploys a Rails service on a Kubernetes cluster for the Plant Coach applications.*

Useful command tidbits during development.

`kubectl exec --stdin --tty <pod-name> -- /bin/bash`

`kubectl exec --stdin --tty plant-coach-be-94f49c475-n8q9v -- /bin/bash `
`/bin/rails c`

`<service-name>.<namespace>.svc.cluster.local`

`kubectl get svc plant-coach-be`
`kubectl describe svc <service>`
