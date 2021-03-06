[![Generic badge](https://img.shields.io/badge/BUILD-PASS-BLUE.svg)](https://shields.io/)

# ansibe-docker-git

## About

An Ansible Playbook which can be used for Building a docker image, Pushing and to Test the image with a docker container.
Advantage of using this playbook is if there is any new commits on Git repo, the playbook will initiate the above tasks. The Playbook is designed in such a way,that the build operations are done on one server and Testing operations on another server.

## Outline

- <b>main.yml</b>
   - Setting Fact Values.
   - Calling tasks, Build and Test based on the condition.

- <b>build.yml</b>
   - Fetching new codes from Git.
   - Creating Docker Image.
   - Taging and Pushing Image to Docker Registry.
  
- <b>test.yml</b>
   - Pull the latest image from the Docker registry, if only there is a new update.
   - Create Docker container with the new image, else task will get skiped.

[<img align="center" alt="Unix" width="800" src="https://raw.githubusercontent.com/ManuGeorge96/ManuGeorge96/master/Tools/jenkns.drawio.png" />][ln]


## Prerequisites

- The git repo must have Docker file and the code section( if needed).
- Idea about configuring Tasks on Jenkins.
- Add Webhook on Git.
 
## To Use The Playbook

### For Running the Playbook Manually

- ```sh
   git clone https://github.com/ManuGeorge96/ansible-docker-git-jenkins.git
  ```
- ```sh
    cd  ansible-docker-git-jenkins
  ```  
- Setting Up Inventory File
  -  Include below line on the <b>hosts</b> file, commend out the existing lines on the file ( edit credentials )
     - ```sh
        [Build]
        build ansible_host=WP_SERVER_IP_HERE ansible_user=SSH_USER_ON_SERVER ansible_ssh_port=SSH_PORT ansible_ssh_private_key_file=PATH_TO_PRIVATE_KEY
        [Test]
        test ansible_host=DB_SERVER_IP_HERE ansible_user=SSH_USER_ON_SERVER ansible_ssh_port=SSH_PORT ansible_ssh_private_key_file=PATH_TO_PRIVATE_KEY
       ```
- Edit Required Data's on <b>main.yml</b> file.
  ```sh
    docker_user: DOCKER_REGISTRY_USER_HERE
    docker_pass: DOCKER_REGISTRY_PASSWORD_HERE
    repo: GIT_REPO_URL
    image_name: IMAGE_NAME
    ct_name: CONTAINER_NAME
    ct_publish_port: PUBLISH_PORT
    ct_port: CONTIANER_PORT
  ```
- ```sh
     ansible-playbook -i hosts main.yml
  ```  
  
## Sample Output from Jenkins

[<img align="left" alt="Unix" width="800" src="https://raw.githubusercontent.com/ManuGeorge96/ManuGeorge96/master/Tools/1.PNG" />][ln]
[<img align="left" alt="Unix" width="800" src="https://raw.githubusercontent.com/ManuGeorge96/ManuGeorge96/master/Tools/2.PNG" />][ln]
[<img align="left" alt="Unix" width="800" src="https://raw.githubusercontent.com/ManuGeorge96/ManuGeorge96/master/Tools/3.PNG" />][ln]
[<img align="left" alt="Unix" width="800" src="https://raw.githubusercontent.com/ManuGeorge96/ManuGeorge96/master/Tools/4.PNG" />][ln]


[ln]: https://www.linkedin.com/in/manu-george-03453613a
