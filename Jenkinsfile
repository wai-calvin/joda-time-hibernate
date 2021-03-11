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
                echo 'Building...'
                sh 'mvn compile'
            }
        }

        stage ('Test') {
            steps {
                echo 'Testing...'
                sh 'mvn test'
            }
        }

        stage ('Deploying') {
            steps {
                sh 'mvn deploy'
            }
        }
    }
}

