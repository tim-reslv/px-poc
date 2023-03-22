Step 1. Check and config secret provider for Portworx if need to test encryption, below is example using K8S secret for encryption
# when use KMS provider AWS KMS 
NAMESPACE=portworx
kubectl -n ${NAMESPACE} create secret generic px-vol-encryption \
  --from-literal=cluster-wide-secret-key=ICAgICAgdHlwZT1ncDMsc2l6ZT0xNTAsZW5jPXRydWUsa21zPWFybjphd3M6a21zOmFwLW5vcnRoZWFzdC0xOjcyMzI4MDU1NDY3MzprZXkvMDRjMGVjYjAtOWQ3Yi00NTljLWJjZjUtMWJhNGM1ZmI0NThjCg

PX_POD=$(kubectl get pods -l name=portworx -n portworx -o jsonpath='{.items[0].metadata.name}')
kubectl exec $PX_POD -n ${NAMESPACE} -- /opt/pwx/bin/pxctl secrets set-cluster-key \
  --secret cluster-wide-secret-key
 
Step 2. Create namespace
kubectl create ns bank-px
 
Step 3. Create JWT
kubectl -n bank-px apply -f jwt/jwt-secret.yaml
 
Step 4. Create bank 
kubectl -n bank-px apply -f .
 
