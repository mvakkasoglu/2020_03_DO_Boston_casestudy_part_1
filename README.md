# Capstone-Project

## CI/CD Pipeline using Jenkins, Ansible, Docker and Kubernetes



**Set up:** 

- Ubuntu 20.04 VM
- Install Git CLI
- Install Docker
- Install minikube
- Install kubectl
- Install Python
- Install PiP via Python
- Install Ansible

Requirements for this project can be found here [document](https://docs.google.com/document/d/17OwlITE-yPWNj3Vi5RtQfz3ItvSkOfnbaVMnzlZyGTg)
 
 
###Steps followed: 

1- Create a respective requirements.txt to download any pip dependencies for this python project.

2- Create a Dockerfile which builds the image.

3- Build and Push image to Dockerhub.

$ docker build -t vakkasoglu/sba-kubernetes-cluster .

$ docker login

Enter YOUR_USERNAME and password when prompted.

$ docker push vakkasoglu/sba-kubernetes-cluster

4- Create a kubernetes.yml which will pull the aforementioned Dockerhub image and create 3 running copies of it.

5- Use the kubernetes.yml to launch your application

$ kubectl create -f kubernetes.yaml

$ kubectl apply -f kubernetes.yaml

Or 

$ kubectl replace --force -f kubernetes.yaml
      
6- Write and run a script to determine the state of your kubernetes cluster including the information about the services, pods, nodes, ip addresses, etc.
upload script to kubernetes-cluster-information.sh
redirect the output of the kuberenetes-cluster-information.sh to kuberenetes-cluster-information-output

$ kubectl get services → displays the services running

$ minikube service <service-name> → application pops-up in the browser

Clean up → $ kubectl delete service <service_name>

-------------------- Make sure Kubernetes run locally successfully --------------------------

7- Create Ansible playbook.yaml file - make sure playbook.yaml file runs ok. (ansible-playbook playbook.yaml) - may need sudo
Starts minikube
Runs command $ kubectl apply -f kubernetes.yaml

8- Start Jenkins in container on VM using the command 

$ docker run -u root --rm -d -p 8080:8080 -p 50000:50000 -v ~/Docker/Jenkins:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins jenkinsci/blueocean

- Configure Jenkins
- Install required plugins (Git, Docker, Pipeline, ShiningPanda, Ansible)
- Configure credentials for Docker

9- Create Jenkinsfile
Jenkinsfile pulls the code from Github, clones it, runs test, builds a new Docker image, pushes the image to DockerHub repository and as the last stage invoke Ansible.



