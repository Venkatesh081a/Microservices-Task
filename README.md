The application consists of four containerized Node.js microservices: User Service, Product Service, Order Service, and Gateway Service. Each service will communicate with one another through Kubernetes Services, and external access will be configured using Ingress.

Application Structure :

The application consists of the following components:

    User Service: Exposed on Port 3000

    Product Service: Exposed on Port 3001

    Order Service: Exposed on Port 3002

    Gateway Service: Exposed on Port 3003

Prerequisites :

    Minikube: Ensure you have Minikube installed

    kubectl: Install the Kubernetes command-line tool to interact with your cluster.

Setting Up the Kubernetes Cluster

    Start Minikube:

        minikube start

    Verify Cluster Status:

        kubectl cluster-info

1. Build all the microservices from the project and push it into the dockerhub.

2. Write the deployment.yml file for each microservices and similarly do it for the service.yml. Finally, write the ingress.yml to create path based routing.

Deploying Microservices

1.  Create Deployment YAML Files:
    Create a directory named deployments and add the following YAML files for each microservice:

        user-service-deployment.yaml

        product-service-deployment.yaml

        order-service-deployment.yaml

        gateway-service-deployment.yaml

Each file should define a Deployment resource for the respective microservice.

2.  Apply Deployments:
    Run the following commands to deploy each service:

        kubectl apply -f deployments/user-service-deployment.yaml
        kubectl apply -f deployments/product-service-deployment.yaml
        kubectl apply -f deployments/order-service-deployment.yaml
        kubectl apply -f deployments/gateway-service-deployment.yaml

3.  Create Service YAML Files:
    Create a directory named services and add the following YAML files for each microservice:

        user-service.yaml

        product-service.yaml

        order-service.yaml

        gateway-service.yaml

    Each file should define a Service resource to expose the respective microservice

4.  Apply Services:
    Run the following commands to create services for each microservice:

        kubectl apply -f services/user-service.yaml
        kubectl apply -f services/product-service.yaml
        kubectl apply -f services/order-service.yaml
        kubectl apply -f services/gateway-service.yaml

Configuring Ingress

1. Install NGINX Ingress Controller:
   Enable the NGINX Ingress controller in Minikube:
   minikube addons enable ingress
2. Create Ingress Resource:
   Create an ingress.yaml file in an ingress directory to define routing rules for your services.
3. Apply Ingress Configuration:
   Apply the ingress configuration using:
   kubectl apply -f ingress/ingress.yaml

Accessing the Application
To access the application through the Gateway Service, use the following command to get the Minikube IP address and port:

minikube service gateway-service --url

Validate Service communication

1. Verify all pods are running :
   kubectl get pods
2. Verify services are created :
   kubectl get svc
3. Verify ingress is configured:
   kubectl get ingress

Access Services via ingress :

User-Service : http://microservices.local/api/users
Product-Service : http://microservices.local/api/products
Order-Service : http://microservices.local/api/orders
Gateway-Service : http://microservices.local/
