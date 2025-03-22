---
title: "Getting started with DevOps 
(my experience)"
datePublished: Mon Jul 08 2024 06:41:18 GMT+0000 (Coordinated Universal Time)
cuid: clycm65vm000g08lehpktgoiv
slug: getting-started-with-devops-my-experience
tags: linux, github, ansible, kubernetes, devops, terraform, cicd, ci-cd, ansible-playbook

---

### What is DevOps?

DevOps is a set of practices that combines software development (Dev) and IT operations (Ops). It aims to shorten the development lifecycle and deliver high-quality software continuously. DevOps emphasizes continious monitoring, testing, automation, and integration between developers and operations teams to improve efficiency, reliability, and speed of software delivery.

### Why we need DevOps?

Practicing DevOps offers several benefits:

1. **Faster Delivery**: Streamlines development and operations, enabling quicker release cycles.
    
2. **Improved Collaboration**: Encourages better communication and collaboration between development and operations teams.
    
3. **Increased Efficiency**: Automation of repetitive tasks reduces manual errors and speeds up processes.
    
4. **Higher Quality Software**: Continuous integration and continuous deployment (CI/CD) practices ensure code is tested and deployed frequently, catching issues early
    

### What is SDLC ?

SDLC stands for Software Development Life Cycle. As a devops engineer our focus should be on automation in building, testing and deployment stage.

![](https://media.geeksforgeeks.org/wp-content/uploads/20231220113035/SDLC.jpg align="center")

### Sign up for a free tier on Amazon AWS

You can create a EC2 instance on AWS using AWS console (you can go with Azure or GCP) in free tier you can run EC2 instance for 750 hours.EC2 instance is nothing but a virtual mechine service provided by AWS. Run the following commands in your linux terminal.

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">ssh -i &lt;path of .pem file&gt; ubuntu@&lt;public ip adress of VM server&gt;</div>
</div>

It will give error that permission is denied change the permissions for .pem file

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">chmod 600 &lt;path of .pem file&gt; // then again run above ssh command</div>
</div>

you will get connected succesfully.

To configure aws run command and create access key from aws console

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">aws configure //give access key and secret key to configure</div>
</div>

### Choose a linux distribution for you

I am having Fedora 40 as my operating system it is important because things become much easier and devops tools have a very good support for linux distribution.

### Shell scripting

Shell scripting is important for automation which is a key thing in devops.Some useful commands for shell scripting are given below

> set -x //for debugging
> 
> ps -ef | grep "gnome" //pipe parameter
> 
> set -e //to exit script on errors
> 
> set -o pipefail //to ensure that script stops on pipefail
> 
> find -name &lt;name of file&gt; //to find the location of file in system

Note: Pipe ( | ) doesn't work with date command because it sends output to STDIN Pipe needs commands not sending info to STDIN.

Note: `curl` command shows you output of logs on terminal where as `wget` stores log in a log file.

### Get used to Version Control

Git is a version control used to push, clone or monitor the github repositories there are various version control systems rather than github such as Subversion, SVN but they are centralized system and github is distrubuted system thus it is more populer

There are some basic git commands

> git init
> 
> git add .
> 
> git commit -m "message"
> 
> git push
> 
> git pull
> 
> git diff
> 
> git log &lt;branch-name&gt;

### What is Ansible ?

Ansible is a tool used for configuration management for the node servers on the cloud there should be a root node to manage other nodes.There should be password less auth between the servers(VM) the easiest way for this is

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">ssh-copy-id</div>
</div>

but sometimes it don't have enough permissions so best way is run below command on root EC2 instance

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">ssh-keygen</div>
</div>

4 files will get created in .ssh folder run the same command in target EC2 instance copy the content of .pub file from root server to authorized\_keys file in target EC2

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720377507569/6fdb2123-ad5b-491c-8a37-4a3e86883f73.png align="center")

Then run the below command on root node

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">ssh &lt;private ip adress of target server&gt;</div>
</div>

And all set you've established password less auth for ansible output should be

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720377862137/b0097c1d-024f-40f3-9202-159292c70ee3.png align="center")

### Ansible roles

For couple of tasks wirh ansible you can run ansible adhoc commands but for more tasks there are ansible playbooks.Ansible adhoc command to create a file on the target server is

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">ansible -i inventory all -m "shell" -a "touch myfile.txt"</div>
</div>

Playbooks are .yaml files that have instructions for task run the following command to run the playbook.Roles are the efficient way to write ansible playbooks it is a set of folders to make manageable and write playbook. The command to create playbook is given below

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">ansible-galaxy role init &lt;Role name&gt;</div>
</div>

to connect your playbook and role add role name under roles in playbook

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720378985620/ff34e203-5821-4c57-add0-0174b93deae4.png align="center")

to run the play book run the below command in your terminal

<div data-node-type="callout">
<div data-node-type="callout-emoji">💡</div>
<div data-node-type="callout-text">ansible-playbook -i &lt;path of inventory file&gt; &lt;playbook name&gt;</div>
</div>

I have used shell module in the adhoc command above you can get the information of other modules on [ansible modules](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html). I have created a ansible role to install and start nginx on ubuntu the repo link is [nginx repo](https://github.com/Ujjwal-Hiranwar/Ansible-tasks).

### What is Terraform?

Let's say you want to shift your cloud infrastructure from one cloud platform to other, now a days organizations use hybrid cloud architecture there Terraform by Hashicrop comes in picture. Here the concept is API as code that is Terraform will talk internally with api of cloud providers, you just have to provide cloud provider and the script you want to run.This concept is also called as Infrastructure as code.