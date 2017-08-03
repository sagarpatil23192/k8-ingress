# k8-ingress
Will help in deploying ingress on GKE.


******* Ingress **************

An Ingress is a collection of rules that allow inbound connections to reach the cluster services.

It can be configured to give services externally-reachable urls, 
load balance traffic ,etc 

It is not a load balancer. But it is a logical controller which will be mapped to LB and it creates routing rules.


1. Create a deployment and service for nginx using the commands given below: 

	a. kubectl run nginx --image=nginx --port=80
	b. kubectl expose deployment nginx --target-port=80 --type=NodePort

	Confirm the same using kubectl get deploy and kubectl get svc

2. Create a deployment and service for echoserver(using a google defined container image) using the commands given below:  


	a. kubectl run echoserver --image=gcr.io/google_containers/echoserver:1.4 --port=8080
	b. kubectl expose deployment echoserver --target-port=8080 --type=NodePort

	Confirm the same using kubectl get deploy and kubectl get svc

3. Now to when you create a ingress resource in kubernetes on GKE, it internally creates a load-balancer in your account. So for thsi POC it is compulsary to use GKE. 

	Run the fanout-ingress.yml using the command given below:

	a. kubectl create -f fanout-ingress.yml --validate=false

        Confirm the same using kubectl get ing and kubectl describe ing fanout-ingress

4. Check your Loadbalncer section in GKE Network window, it will have a load balancer. 

5. Wait for some time and hit the IP of Loadbalancer.

	Hitting just the IP will direct you to Nginx service and hitting IP/echo will direct you to echoserver service.






