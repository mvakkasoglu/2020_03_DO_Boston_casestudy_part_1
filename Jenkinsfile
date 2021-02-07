pipeline {
	agent any
	environment {
	    DOCKER_HUB_REPO = "vakkasoglu/capstone-project"
		CONTAINER_NAME = "capstone-project"
		REGISTRY_CREDENTIAL = "dockerhub"
	}
	stages {
		stage('Set up') {
			steps {
				script {
					sh 'rm -rf  2020_03_DO_Boston_casestudy_part_1'
				}
			}
		}
		stage('SCM Checkout') {
			steps {
				script {
					sh 'git clone https://github.com/mvakkasoglu/2020_03_DO_Boston_casestudy_part_1.git'
				}
		    }
		}
		stage('Build docker image') {
			steps {
				script {
					dir('./2020_03_DO_Boston_casestudy_part_1') {
						sh 'docker image build -t $DOCKER_HUB_REPO:latest .'
						sh 'docker image tag $DOCKER_HUB_REPO:latest $DOCKER_HUB_REPO:$BUILD_NUMBER'
					} 
				}
			}
		}
	    stage('Push docker image') {
		    steps {
			    script {
				    dir('./Boston_casestudy_part_1') {
				        docker.withRegistry( '', REGISTRY_CREDENTIAL ) {
				            sh 'docker push vakkasoglu/capstone-project:$BUILD_NUMBER'
				            sh 'docker push vakkasoglu/capstone-project:latest'
			            }
				    }
	            }
			}
		}
		//stage ('deploy') {
		//	steps {
		//		ansiblePlaybook(playbook: 'ansible-playbook.yml')
		//		//sh 'ansible-playbook ansible-playbook.yml'
		//		
		//	}
	    //}
	}
}