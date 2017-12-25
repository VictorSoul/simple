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
              sh 'mv -u target/demo-0.0.1-SNAPSHOT.war  docker/demo.war'
            }
        }
        stage('Build') {
            steps {
             sh "docker build -t demo:${GIT_BRANCH} docker/"
        	}
        }
        stage('Push') {
            steps {
             sh 'pwd'
             sh "docker tag demo:${GIT_BRANCH} 10.39.201.68:5000/demo:${GIT_BRANCH} "
             sh "docker push 10.39.201.68:5000/demo:${GIT_BRANCH}"
            }
        }
    }
}