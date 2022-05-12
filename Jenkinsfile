#!/usr/bin/env groovy
pipeline {
    agent any

    tools {
         maven 'MAVEN'
    }

    stages{
	    stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
		}
        stage('Clean Install') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
				stash(name: "deployable", includes: 'target/*.war')
				
            }
         }
        stage('Deploy') {
            steps {
				unstash("deployable")
                echo 'Deploy somewhere!'
				archiveArtifacts 'target/*.war'
				
				sshagent(['webfiles']) {
			    sh 'ssh ec2-user@34.245.42.100 pwd'
			    sh 'ssh ec2-user@34.245.42.100 rm /var/www/html/cicdapp.war'
				sh 'scp ./cicdapp.war ec2-user@34.245.42.100:/var/www/html'
				}
            }
        }
    }
}
