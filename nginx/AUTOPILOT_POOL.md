Step 1. Apply AutoPilot rule
kubectl apply -f autopilotrule-pool-expand-example.yaml
 
Step 2. Wait Portworx to auto expend

Step 4. Monitor and check autopilot pod log
 
Step 3. Verify with pxctl command
kubectl -n portworx exec px-cluster-28be18a2-7bf3-471e-b59e-ed1ac9aceea0-hzzx8 -- bash -c "/opt/pwx/bin/pxctl v l"

