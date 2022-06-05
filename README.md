# Sonarqube Task

## Install SonarQube Using Helm Chart
```sh 
helm repo add sonarqube https://SonarSource.github.io/helm-chart-sonarqube
```
```sh 
helm repo update
```
```sh 
kubectl create namespace sonarqube
```
- Pull Chart to edit servece in values.yaml from ClusterIp To NodePort:
```sh 
helm pull sonarqube/sonarqube
```
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/5.png)

- Install and Upgrade with the new values.yaml file
```sh
helm upgrade -f values.yaml  --install -n sonarqube sonarqube sonarqube/sonarqube
```
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/8.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/9.png)

### Steps To Install Jenknis and Intgrate with Sonar Qube:
- change path in jenkins-pv.yaml file to path in your machine
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/10.png)

- Apply jenkins resources in /apply-jenknis/jenkins dir run:
```sh
kubectl apply -f .
```
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/12.png)
- Check Logs to get password of jenkins to configure
```sh
kubectl logs -f {POD_NAME} -n jenkins
```
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/13.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/15.png)

- Install SonarQube and NodeJS Plugins
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/16.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/23.png)
- Create Token for SonarQube in Jenkins
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/17.png)

- Configure SonarQube Plugin
1- Create Credentials for  SonarQube using token created above
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/19.png)
2-  Configure Sonarqube Server Dashboard -> configuration
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/21.png)
3- Configure SonarQube Scanner and NodeJS  From Dashboard -> Global tool configuration
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/20.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/24.png)

3-  Create Pipeline to test code of this  [REPO](https://github.com/moutazmuhammad/nodejs_sonerqube.git) Using SonarQube
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/22.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/25.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/26.png)


- Install Multi Branch Plugin
1- Edit values.yaml file
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/27.png)
2- Install with upgrade plugin
```sh
helm upgrade -f values.yaml  -n sonarqube sonarqube sonarqube/sonarqube \
 --set "plugins.install={https://github.com/mc1arke/sonarqube-community-branch-plugin/releases/download/1.11.0/sonarqube-community-branch-plugin-1.11.0.jar}" 
```
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/29.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/30.png)
![Build Status](https://raw.githubusercontent.com/moutazmuhammad/sonerqube_task/main/img/31.png)



