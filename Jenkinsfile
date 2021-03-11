#!/bin/env groovy

pipeline {

    agent any

    tools { 
        maven 'apache-maven-3.6.3' 
        jdk 'jdk9' 
    }

    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }

        stage ('Build') {
            steps {
                echo 'This is a minimal pipeline.'
                sh 'mvn compile'
            }
        }
    }
}


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