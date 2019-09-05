pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2 -e NEXUS_VERSION = "nexus3",NEXUS_URL = "127.0.0.1:8081",NEXUS_REPOSITORY = "poc-maven",NEXUS_CREDENTIAL_ID = "nexus-credentials"'
                       
                    }
    }
    stages {
        stage('Build') 
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
            stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
