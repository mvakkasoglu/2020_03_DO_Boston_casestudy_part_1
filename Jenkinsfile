pipeline {
	agent {
		docker {
			image 'python:3.7.2'
			args '-u root'
		}
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
					sh 'git clone https://github.com/mvakkasoglu/2020_03_DO_Boston_casestudy_p
