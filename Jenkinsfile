pipeline {
    agent any 
    tools {
        maven 'M3' 
    }
    stages {
        stage('Checkout') {
            steps {
                // En Pipeline as Code, cette étape devient automatique !
                // Jenkins télécharge tout seul le dépôt qui contient le Jenkinsfile.
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }
        stage('Run') {
            steps {
                withEnv(['JENKINS_NODE_COOKIE=dontKillMe']) {
                    bat 'start "PetClinic" java -jar target/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar --server.port=8081'
                }
            }
        }
    }
}
