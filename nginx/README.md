Step 1. kubectl create ns nginx
Step 2. kubectl -n nginx apply -f readwritemany-pvc.yaml
Step 3. kubectl -n nginx apply -f nginx-deployment.yaml
 
Step 4. Write file to one Pod mounted RWX PV
kubectl -n nginx exec nginx-69d4db8dd8-8g4tn -- bash -c "echo abcd > /usr/share/nginx/html/testing.html"
 
Step 5. Verify Result ( 3 pods)
kubectl -n nginx exec nginx-69d4db8dd8-8g4tn -- bash -c "cat /usr/share/nginx/html/testing.html"
kubectl -n nginx exec nginx-69d4db8dd8-n2bz9 -- bash -c "cat /usr/share/nginx/html/testing.html"
kubectl -n nginx exec nginx-69d4db8dd8-xbrjt -- bash -c "cat /usr/share/nginx/html/testing.html"
 
Step 6. Update file content in RWX PV
kubectl -n nginx exec nginx-69d4db8dd8-8g4tn -- bash -c "echo 1234 > /usr/share/nginx/html/testing.html"
 
Step 7. Verify Result ( 3 pods)
kubectl -n nginx exec nginx-69d4db8dd8-8g4tn -- bash -c "cat /usr/share/nginx/html/testing.html"
kubectl -n nginx exec nginx-69d4db8dd8-n2bz9 -- bash -c "cat /usr/share/nginx/html/testing.html"
kubectl -n nginx exec nginx-69d4db8dd8-xbrjt -- bash -c "cat /usr/share/nginx/html/testing.html"
