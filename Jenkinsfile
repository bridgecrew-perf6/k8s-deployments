pipeline {
 agent none
 parameters {
   string(name: 'ECRURL', defaultValue: '224587543863.dkr.ecr.ap-south-1.amazonaws.com', description: 'Please Enter ECR REGISTRY URL')
   string(name: 'IMAGE', defaultValue: 'demowebapp:3', description: 'Please Enter the Image to Deploy?')
   password(name: 'PASSWD', defaultValue: '', description: 'Please Enter your Gitlab password')
 }
 stages {
  stage('Deploy')
  {
    agent { label 'demo' }
    steps { 
        git credentialsId: 'GitlabCred', url: 'https://gitlab.com/dineshdevops36/deployments.git'
	 	dir ("./k8smanifest") {
	      sh "sed -i 's/image:.*/image: $ECRURL$IMAGE/g' deployment.yaml" // make sure the ECRURL has \/ at the end
	    }
		sh 'git commit -a -m "New deployment for Build $IMAGE"'
		sh "git push https://dineshdevops36:$PASSWD@gitlab.com/dineshdevops36/deployments.git"
    }
  }
 }
}
