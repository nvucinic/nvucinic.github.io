# Install Helm 

Install Helm on to your local machine depending on your local OS. To do this, refer to See [Helm install steps](https://docs.helm.sh/using_helm/#installing-helm) 

Initialize Helm on both your server and client with this command:
```sh
helm init
```
Please make sure your local system is authenticated to use kubectl.
This will install tiller on the Kubernetes cluster which is a server side component that stores all your deployment version for easy rollbacks or rollforwards

# Configure service account for Helm in GKE



Run the following commands to setup and configure tiller to use this service account

```sh
kubectl create serviceaccount --namespace kube-system tiller
kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'
helm init --service-account tiller --upgrade
```