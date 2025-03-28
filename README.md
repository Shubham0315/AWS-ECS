# AWS-ECS
Elastic Container Service(ECS), a Container orchestration service to simplify the deployment, management, and scaling of containerized applications.

- It is Container Orchestration Environment like K8S.
- Docker is a container platform which allows to manage lifecycle of containers. If we've VM on top of which we install docker using which we can run containers
  - We can run our application using docker and expose to our end users. Then why K8S or ECS?
  - As we know in docker we have fundamental issues like auto healing and auto scaling not included.
  - If auto healing is not there and our container is down due to some reason or someone deleted it, the end user will be unable to access the application (Containers are ephemeral). So end user can face app downtime
  - While running container, they use resources from host system with minimal own dependencies. If there are multiple containers, resources like CPU, memory from host are shared amongst containers. If traffic on our website increase, containers on our VM wont be able to handle traffic as here docker dont have auto scaling capability. So customer will see downtime
  - Even if we heal our stopped container and bring it up, its IP address will be changed. So if anyone tries to access container on our IP address, he will face downtime
 
- So main issues with containers are :-
  - Auto scaling not enabled
  - Auto healing not enabled
  - Changing IPs of containers
 
Thats why evolution of container orchestration solutions has taken place
- 

----------------------------------------------------------------------------------------

Evolution of Containers
-
- Kubernetes solved auto healing and auto scaling issues of docker.
- If containers goes down, K8S comes up with controllers to bring in Auto Healing. 
- Using HPA or VPA, CRDs it also solved problem of Auto Scaling
- For the IP addresses changing frequently, using services, SVC discovery we can solve the issue

- So using K8S we can take these containers to production use cases whereas in docker containers were being used but restricted to development env only
- K8S being Open Source, people started building solutions on top of it like EKS, AKS, GKE, etc

----------------------------------------------------------------------------------------

Elastic Container Service (ECS)
-
- In AWS, ECS is there similar to K8S
- In ECS there wont be concepts like pos, deployments. It will use own concepts like tasks, clusters, services.
- ECS platform developed by AWS will be restricted to only AWS customers and services and it will not be open source
- If we move out of ECS to Azure, we cant use resources created on AWS. In world of hybrid cloud, we dont know when we have to move resources(acc to business requirements). We cant resuse the resources created in ECS into other platform.
- Here advantage offered by AWS is when moving from one platform to other, the company will have to rethink as they've lot of workload on ECS. So its maintenance overhead.
- K8S keeps updating daily due to its community support. But ECS doesn't have all features which K8S have which is a drawback of ECS.
- e.g :-
  - K8S have concept of Custom Resource Definition (CRDs), where K8S allows us to extend its capabilities by submitting CRs after creation
  - Using CRD if we feel something need to be modified, we can build our own controller (CR/CRD) and submit it to K8S to extend capabilities of K8S. This is where community plays critical role and extend K8S
  - This concept of CRD is not there on ECS, so its behind K8s.
  - Also, on K8S we can configure lot on ingress rules and controllers using which we can add capabilities such as LB
  - Thus ECS is good container orchestration env but lacks some features stated above
 
- Elastic K8S Service (EKS) is managed service by AWS. So many organizations use EKS on top of ECS

Advantages of ECS
-
- We dont have to manage anything. AWS will give us cluster and will support server(EC2) and serverless(fargate) models. If we use serverless fargate with ECS (just like lambda), we dont have to manage anything in our env. Using EC2 we need to attach EC2 with ECS.
- Very simple in nature. K8S has very complicated architecture master and worker node. If we are not using EKS, using just minikube K8S we've to take care of all things. On ECS, if we want to run our app using ECS, we just have to create task definition(CR) which will create task and we can start using it. We can also create a service and integrate LB with it
- Using fargate, we dont need to care avout anything, CRs will get created on their own


