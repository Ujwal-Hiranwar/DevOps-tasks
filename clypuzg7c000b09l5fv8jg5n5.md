---
title: "Project management and Containerisation in devops"
datePublished: Wed Jul 17 2024 13:09:02 GMT+0000 (Coordinated Universal Time)
cuid: clypuzg7c000b09l5fv8jg5n5
slug: project-management-and-containerisation-in-devops
tags: docker, javascript, angularjs, nodejs, kubernetes, devops, containers, kubectl, docker-images

---

## AGILE Methodology

The Agile methodology is **a project management approach that involves breaking the project into phases and emphasizes continuous collaboration and improvement**. Teams follow a cycle of planning, executing, and evaluating.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1721223608057/cc734780-038f-4886-8145-c3d1d279b994.png align="center")

## Project Management : JIRA

JIRA is a popular project management tool developed by Atlassian, widely used for issue tracking and agile project management. Here are some key points about JIRA:

1. **Issue Tracking**: JIRA allows teams to create, track, and manage issues, tasks, bugs, and other work items.
    
2. **Agile Project Management**: Supports agile methodologies such as Scrum and Kanban, with features like customizable boards, backlogs, sprints, and burndown charts.
    
3. **Customization**: Highly customizable with configurable workflows, fields, and issue types to fit various project needs.
    
4. **Integration**: Integrates with numerous tools, including Confluence, Bitbucket, GitHub, Slack, and many CI/CD tools.
    
5. **Reporting**: Offers robust reporting and dashboard capabilities to track project progress, team performance, and other key metrics.
    
6. **Automation**: Features automation rules to streamline repetitive tasks and enhance productivity.
    
7. **Security**: Provides strong security controls and compliance with industry standards.
    

JIRA is widely used by software development teams, IT service management, and other industries for efficient project management and collaboration.

## Containerization : Docker and Kubernetes

### Docker

Docker solve a simple problem that "It is running on your system but not in mine.The concept here is you simply put all the necessary things for your application in one container having a image, You can relate image with a operating system where the things that are necessary for your application installed by the developer itself so that it will be independent of other variables of outer surrounding.

Install `docker desktop` from their website [docker-desktop](https://www.docker.com/products/docker-desktop/) and sign up on [dockerhub.com](https://hub.docker.com/), below is the command to create a image. Here . represent that docker file is in current directory.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">docker build -t &lt;image name&gt; .</div>
</div>

Below is the command to run the container having the image that we have made above here -d means we want to run in detach mode. We have to expose the port inside the docker and tell our system that allocate this specific port to the container. The port on left side is local machine port and port on right side is the port we have to expose. This is called port mapping.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">docker run -d -p &lt;port of machine &gt;:&lt;port inside container&gt; &lt;image name&gt;</div>
</div>

To list the docker containers and docker images use below command

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">docker containers ls -a</div>
</div>

If you are using Linux then to start docker engine, run below command in your Linux terminal for windows just run docker desktop.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">systemctl --user start docker-desktop</div>
</div>

### Kubernetes

There are some features missing in docker such as auto healing of containers, support of enterprise level standards, multiple node architecture ,load balancing etc. Here the concept is there is one master node and multiple worker nodes. we will use master node to communicate with worker nodes

So here kubernetes comes in picture which is developed by google which is also known as K8's.Kubernetes is like wrapping your containers with pods so that the Master node can communicate with that container.

Kubernetes have multiple node architecture which prevents container killing, it have replication controller which implements load balancing and it have auto healing.

we have to install `kubectl` from [Kube-ctl](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/) and `Minikube` from [minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)

Run the below command to create a docker container and it also download kubernetes and configure kube-ctl

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">minikube start</div>
</div>

To create the resources use the below command

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">kubectl apply -f &lt;your web.yaml file name&gt;</div>
</div>

to get the pods name use below command

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">kubectl get pod -o wide</div>
</div>

to start the service after creating all the resources run the below command

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">minikube service &lt;your service name&gt;</div>
</div>

So, This is how you can integrate your app with kubernetes. but, this is not this simple there are things way beyond that in the world of kubernetes.