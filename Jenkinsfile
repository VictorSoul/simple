pipeline {
    agent any

    stages {
    	stage('Sonar') {
            steps {
            sh 'pwd'
              sh 'sonar-scanner'
            }
        }
        stage('Package') {
            steps {
              sh 'mvn clean package'
              sh 'mv -u target/simple-0.0.1-SNAPSHOT.war  docker/simple.war'
            }
        }
        stage('Build') {
            steps {
             sh "docker build -t simple:${GIT_BRANCH} docker/"
        	}
        }
        stage('Push') {
            steps {
             sh "docker tag simple:${GIT_BRANCH} 10.39.107.141:5000/simple:${GIT_BRANCH} "
             sh "docker push 10.39.107.141:5000/simple:${GIT_BRANCH}"
            }
        }
    }
}