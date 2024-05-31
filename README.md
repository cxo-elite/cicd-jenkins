

---------
Final Demo
---------

Jenkins Admin password
--------------
admin
3628b649ffc542e68ae308d5c6ac2994

Jenkins Pipeline - http://3.7.201.232:8080/
Prod - AWS Web App - http://3.7.201.232:8005/docs
Local - Web app http://127.0.0.1:8005/docs
Git - https://github.com/cxo-elite/cicd-jenkins
AWS EC2 - https://ap-south-1.console.aws.amazon.com/ec2/home?region=ap-south-1#Instances:instanceState=running
Mail 
AWS EC2 Machines 1. App Server" -  ssh -i "aws-ec2-key.pem" ubuntu@3.7.201.232
                  2. Monitoring Server" - ssh -i "aws-ec2-key.pem" ubuntu@13.200.109.82
CM - Prometheus - http://13.200.109.82:9090/targets?search=
                  Server metrics - 13.200.109.82:9100/metrics
                  Fast api app metrics - http://13.200.109.82:8005/docs 
     Grafhana - http://13.200.109.82:3000/dashboard/new?orgId=1&from=1717079455746&to=1717083055746&viewPanel=1
                http://13.200.109.82:3000/dashboard/new?orgId=1&refresh=auto
                


Local to Git
----------
cd D:\Git\ai_projects\mlops_bootcamp\ml-ci-cd-jenkins\cicd-jenkins
git status -- Identify the changes in code
git add .
git commit -m "Test file added"
git branch -M main
git push -u origin main



=======================================================
Demo codes
----------

Local Docker
-----------
Start modelv1 container
command: Start loan prediction app 
docker exec -d -w /code modelv1 python main.py

http://127.0.0.1:8005/docs
Post the requirement details in Json format

PROD - Connect to ec2
-------------
ssh -i "aws-ec2-key.pem" ubuntu@3.7.201.232

remove existing docker image
docker stop modelv1
docker rm modelv1

Deploy
------------
Execute first job in jenkins pipeline

Fast api
---------------
http://3.7.201.232:8005/docs

{
  "Gender": "Male",
  "Married": "No",
  "Dependents": "2",
  "Education": "Graduate",
  "Self_Employed": "No",
  "ApplicantIncome": 5849,
  "CoapplicantIncome": 0,
  "LoanAmount": 1000,
  "Loan_Amount_Term": 1,
  "Credit_History": "1.0",
  "Property_Area": "Rural"
}


Git changes
-----------
cd D:\Git\ai_projects\mlops_bootcamp\ml-ci-cd-jenkins\cicd-jenkins
git status -- Identify the changes in code
git add .
git commit -m "Test file added"
git branch -M main
git push -u origin main

================================================================

# Setup Virtual Environment
====================================================================================

```python
conda create -n jenkins-env python=3.10 -y
conda activate jenkins-env
pip install -r src/requirements.txt
pip install src/.
```

# Test the FASTAPI

```json

{
  "Gender": "Male",
  "Married": "No",
  "Dependents": "2",
  "Education": "Graduate",
  "Self_Employed": "No",
  "ApplicantIncome": 5849,
  "CoapplicantIncome": 0,
  "LoanAmount": 1000,
  "Loan_Amount_Term": 1,
  "Credit_History": "1.0",
  "Property_Area": "Rural"
}


```

# Docker Commands
```
docker build -t loan_pred:v1 .
docker build -t manifoldailearning/cicd:latest . 
docker push manifoldailearning/cicd:latest

docker run -d -it --name modelv1 -p 8005:8005 manifoldailearning/cicd:latest bash

============================================================

docker build -t loan_pred:v1 .
docker build -t cxo4elite/cicd:latest . 
docker push cxo4elite/cicd:latest

docker run -d -it --name modelv1 -p 8005:8005 cxo4elite/cicd:latest bash

docker exec modelv1 python prediction_model/training_pipeline.py

docker exec modelv1 pytest -v --junitxml TestResults.xml --cache-clear

docker cp modelv1:/code/src/TestResults.xml .
===========================================================

docker exec modelv1 python prediction_model/training_pipeline.py

docker exec modelv1 pytest -v --junitxml TestResults.xml --cache-clear

docker cp modelv1:/code/src/TestResults.xml .

docker exec -d -w /code modelv1 python main.py

docker exec -d -w /code modelv1 uvicorn main:app --proxy-headers --host 0.0.0.0 --port 8005


```

# Installation of Jenkins

```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins

sudo apt update
sudo apt install fontconfig openjdk-17-jre
java -version

sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

`
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
`

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Add the repository to Apt sources:
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo usermod -a -G docker jenkins
sudo usermod -a -G docker $USER

```

# Admin password Jenkins

`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

# Payload URL format in github repo webhook

`http://<public-ipv4 address>:8080/github-webhook/` #replace it with ur own public-ipv4 address

```

# Additional Improvements

docker remove $(docker ps -a -q)
docker images --format "{{.ID}} {{.CreatedAt}}" | sort -rk 2 | awk 'NR==1{print $1}'



# Create Stage Branch
`git checkout -b staging`
`git push `

==================================================
Test Modification

#AWS connect to instance
ssh -i "aws-mlops.pem" ubuntu@ec2-43-205-241-33.ap-south-1.compute.amazonaws.com


Docker commands
----------------

-- If training buil need to run mumltiple times stop and remove the docker container and then build
docker stop modelv1
docker rm model v1

====================================================================================
Demo
----

