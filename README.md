Istio Project 

Purpose: 
1, To study about Istio using Minikube and sample microservices applications in GCP 

Lession Learnts 
1, Istio installration is quite easy and deploy envoy proxy to each pods are easy because i do not need to have any configration for kubernetes. 
2, Istio multiple addons that enable me to visualize the microservice status. 


Cluster
Local Minikube Cluster 
Istio version
istio-1.14.3

// initialize minikube cluster with required resources.
minikube start --cpus='6' --memory='7000'
//install Istio
mkdir istio-study
cd istio-study
curl -L https://istio.io/downloadIstio | sh -
cd istio-1.14.3		
//Make intio command excutable 
export PATH=$PATH:/Users/shoya.suzuki/go/src/istio-study/istio-1.14.3/bin
//Confirm you can use istio ctl 
istioctl —help 
if you can install istion well, you can see some of the output. 

kubectl get ns 
istioctl install
// confirm the istio namespace installed well 
kubectl get pod -n istio-system

// clone manifest file from GCP demo to make sample microservices applications
//download kubernetes-manifests file from here https://github.com/GoogleCloudPlatform/microservices-demo/tree/main/release 
kubectl apply -f microservices-demo/release/kubernetes-manifests.yaml

// to know current namespace label 
kubectl get ns defalt —show-labels 
// edit the labels with configured istio 
kubectl label  namespace default istio-injection=enabled
// delete the pods we just created 
kubectl delete -f microservices-demo/release/kubernetes-manifests.yaml
kubectl get pod 
// reapply the kubernetes manifests file 
kubectl apply -f microservices-demo/release/kubernetes-manifests.yaml

Then all pods have 2 container which are envoy proxy 


kubectl apply -f istio-1.14.4/samples/addons/
kubectl get svc -n istio-system
kubectl port-forward svc/kiali -n istio-system 20001
 then we can get the address for kiali GUI

App labels in Pods for Istio 
Istio injection havs to have pods which has “app” labels you need to keep in mind 
