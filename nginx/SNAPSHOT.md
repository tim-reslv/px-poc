Step 1. List volume
kubectl -n portworx exec px-cluster-28be18a2-7bf3-471e-b59e-ed1ac9aceea0-gk8ht -- bash -c "/opt/pwx/bin/pxctl v l"
 
Step 2. Create snapshot
kubectl -n portworx exec px-cluster-28be18a2-7bf3-471e-b59e-ed1ac9aceea0-gk8ht -- bash -c "/opt/pwx/bin/pxctl volume snapshot create --name nginx_snapshot 416512645964610006"
 
Step 3. Check current html content
kubectl -n nginx exec nginx-69d4db8dd8-8g4tn -- bash -c "cat /usr/share/nginx/html/testing.html"
 
Step 4. Modify file after take snapshot
kubectl -n nginx exec nginx-69d4db8dd8-8g4tn -- bash -c "echo xyzf > /usr/share/nginx/html/testing.html"
 
Step 5. Check current html content again
kubectl -n nginx exec nginx-69d4db8dd8-8g4tn -- bash -c "cat /usr/share/nginx/html/testing.html"
 
Step 6. Scale down pod before restore snapshot
kubectl -n nginx scale --replicas=0 deployment/nginx
 
Step 7. Restore snapshot
kubectl -n portworx exec px-cluster-28be18a2-7bf3-471e-b59e-ed1ac9aceea0-gk8ht -- bash -c "/opt/pwx/bin/pxctl volume restore --snapshot nginx_snapshot 416512645964610006"
 
Step 8. Check current html content again (new pod id)
kubectl -n nginx exec nginx-69d4db8dd8-klpv5 -- bash -c "cat /usr/share/nginx/html/testing.html"
 
