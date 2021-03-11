pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'export MAVEN_HOME=/Users/cwai/Downloads/apache-maven-3.6.3'
                sh 'export PATH=$PATH:$MAVEN_HOME/bin'
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            steps {
                echo "deploying..."
            }
        }
    }
}