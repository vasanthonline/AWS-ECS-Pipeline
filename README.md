# Node.js API to AWS ECS

## Application deployed [here](ec2-3-15-190-149.us-east-2.compute.amazonaws.com)

## Setup AWS Instance
* Sign up / create account at https://aws.amazon.com/
* Navigate to Services -> Elastic Container Service
  * Navigate to Repositories under ECR (Elastic Container Registry)
  * Create Repository
    * Click "View Push Commands" and use the commmands listed to build, tag, and push your image to the aws registry
* Navigate to Services -> Elastic Container Service
 * Navigate to Clusters under ECS (Elastic Container Service)
   * Create Cluster
     * EC2 Linux + Networking
     * Provisioning Model: On-Demand Instance
     * EC2 Instance Type: t2.micro
     * Number of Instances: 1
     * EC2 Ami Id: Amazon Linux 2 AMI (going with default, need to research more about what this is)
     * EBS Storage (GiB): 22
     * Select/Create key pair in order to allow SSH access into EC2 instance
     * VPC: Default
     * Subnets: Default
     * Security Group: Default (Check rules to define inbound/outbound rules, like SSH -> port 22, HTTP/HTTPS)
     * Container Instance IAM Role: Default
* Navigate to Services -> Elastic Container Service
 * Navigate to Task Definitions under ECS (Elastic Container Service)
   * Create New Task Definition
     * EC2
     * Container Definitions (Add desired container that was uploaded)
      * Image should be the URI of the image we created earlier, but add ":latest" to fetch the latest image
      * Memory Limit: 256 Hard Limit (need to research more about what this is)
      * Port Mappings: Map 80 (host) to 3000 (container); TCP
      * Entrypoint, Command, and Working directory should've been set in Dockerfile (need to research env variables)
      * Configure for JSON if wanting to do any automation ;)
* Navigate to Services -> Elastic Container Service
 * Navigate to Clusters under ECS (Elastic Container Service)
   * Cluster you created -> Tasks -> Run New Task -> Run Task
   * Cluster you created -> ECS Instances -> Click the EC2 Instance
   * Access service by grabbing the public DNS

## Continuous Deployment
Before starting workflow, navigate to the AWS console and stop the currently running container so that this workflow can work. We have to do this because dynamic port mapping needs to be configured in order to truly have continuous deployment. 

Explanations for this can be found here:

https://stackoverflow.com/questions/48931823/i-cant-deploy-a-new-container-to-my-ecs-cluster-because-of-ports-in-use

https://aws.amazon.com/premiumsupport/knowledge-center/dynamic-port-mapping-ecs/

## Resources Used
https://www.freecodecamp.org/news/how-to-deploy-a-node-js-application-to-amazon-web-services-using-docker-81c2a2d7225b/

https://www.youtube.com/watch?v=KJNj37ZXPqE&t=2360s

https://www.youtube.com/watch?v=9K3OEhm2lR0
