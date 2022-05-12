#!/usr/bin/env groovy
pipeline {
    agent any

    tools {
         maven 'MAVEN'
		 jdk 'JDK'
    }

    stages{
	    stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        stage('Compile') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                archiveArtifacts 'target/*.xml'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
                archiveArtifacts 'target/*.war'
            }
         }
        stage('Deploy') {
            steps {
                echo 'Deploy somewhere!'
            }
        }
    }
}
