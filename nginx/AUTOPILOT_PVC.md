Step 1. Apply AutoPilot rule
kubectl apply -f autopilotrule-example.yaml
 
Step 2. Monitor
watch kubectl get events --field-selector involvedObject.kind=AutopilotRule,involvedObject.name=volume-resize --all-namespaces --sort-by .lastTimestamp
 
Step 3. Generate file in mounted PV to trigger auto expend
kubectl -n nginx exec -it nginx-69d4db8dd8-8tpd6 bash
dd if=/dev/urandom of=/usr/share/nginx/html/700m.bin bs=1024 count=71680
 
Step 4. Wait Portworx to auto expend
 
Step 5. Verify with pxctl command, or check autopilot pod log
kubectl -n portworx exec px-cluster-28be18a2-7bf3-471e-b59e-ed1ac9aceea0-hzzx8 -- bash -c "/opt/pwx/bin/pxctl v l"

