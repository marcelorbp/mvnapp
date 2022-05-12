#!/usr/bin/env groovy
pipeline {
    agent any

    tools {
         maven 'MAVEN'
    }

    stages{
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
