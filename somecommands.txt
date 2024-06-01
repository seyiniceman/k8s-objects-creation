
#To enter inside a container
kubectl exec -it <pod_name> -n <namespace> -- /bin/sh

#Write A file in the default nginx path inside the container

cat <<EOF > /usr/share/nginx/html/test.html 
<!DOCTYPE html>
<html>
    <head>
        <title>This is A Test</title>
    </head>
    <body>
        <h1 style="color: chocolate;">Hello Replica Service!!</h1>
        <h2>Congratulations, You Are Doing Well :-)</h2>
    </body>
</html>
EOF


#To Apply The Dashboard Run
kubectl apply -f kubernetes-dashboard.yaml

#Create an annonymous user to access the dashboard
kubectl create clusterrolebinding cluster-system-anonymous --clusterrole=cluster-admin --user=system:anonymous

#Accessing the Dashboard –The dashboard can be accessed from your local browser by going to the below link –
https://masterpublicipaddreess:6443/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

#In the above URL the Public IP/DNS name of the master EC2 should be replaced and 6443 is the port number to access the Dashboard.

#Upon browsing to the URL, you will be prompted to enter the credentials to login the dashboard as shown below : use this command to generate a token
kubectl create -n kubernetes-dashboard token admin-user

