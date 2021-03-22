#!/bin/env groovy

pipeline {

    agent any

    parameters {
        string(name: 'ARTIFACTORY_SERVER', defaultValue: 'joda-time-hibernate')
        string(name: 'SERVER_URL', defaultValue: '')
        string(name: 'MAVEN_TOOL', defaultValue: 'apache-maven-3.6.3')
        password(name: 'USER', defaultValue: 'SECRET')
        password(name: 'PASSWORD', defaultValue: 'SECRET')
    }

    tools {
        // Install the Maven version configured as "mmaven" and add it to the path.
        maven params.MAVEN_TOOL
    }

    environment {
        JFROG_CLI_BUILD_NAME = "${env.JOB_NAME}"
        JFROG_CLI_BUILD_NUMBER = "${env.BUILD_NUMBER}"
    }

    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/wai-calvin/joda-time-hibernate.git'
            }
        }
        
        stage('Test') {
            steps {
                // Run Maven on a Unix agent.
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        
        stage('Deploy') {
            when {
                branch 'master'   
            }
            steps {
                junit '**/target/surefire-reports/TEST-*.xml'
                archiveArtifacts 'target/*.jar'
                sh "jfrog rt u 'target/*.jar' $params.ARTIFACTORY_SERVER --url=$params.SERVER_URL --user=$params.USER --password=$params.PASSWORD"
            }
        }
    }

    // tools { 
    //     maven 'apache-maven-3.6.3' 
    //     jdk 'jdk9' 
    // }

    // stages {
    //     stage ('Initialize') {
    //         steps {
    //             sh '''
    //                 echo "PATH = ${PATH}"
    //                 echo "M2_HOME = ${M2_HOME}"
    //             ''' 
    //         }
    //     }

    //     stage ('Build') {
    //         steps {
    //             echo 'Building...'
    //             // sh 'mvn compile'
    //             sh 'git clone https://github.com/wai-calvin/joda-time-hibernate.git'
    //         }
    //     }

    //     stage ('Test') {
    //         steps {
    //             echo 'Testing...'
    //             sh 'mvn test'
    //         }
    //     }

    //     stage ('Deploying') {
    //         steps {
    //             sh 'mvn deploy'
    //         }
    //     }
    // }
}

