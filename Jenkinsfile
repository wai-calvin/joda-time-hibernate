pipeline {
    agent none

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3.6.3'
                }
            }
            steps {
                sh 'export M2_HOME=/Users/cwai/Downloads/apache-maven-3.6.3' 
                sh 'export PATH=$PATH:$M2_HOME/bin'
                sh 'mvn --version'
                sh 'mvn compile'
            }
        }

        // stage('Test') {
        //     steps {
        //         sh 'mvn test'
        //     }
        // }

        // stage('Deploy') {
        //     steps {
        //         echo "deploying..."
        //     }
        // }
    }
}