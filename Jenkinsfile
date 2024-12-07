pipeline {
     environment{
        dockerimage=""
    }
    agent any
    stages {
        stage('Git clone') {
            steps {
            git branch: 'master',url: 'https://github.com/madhav0407/TicketResolver_Backend.git'
            }
        }

        stage("Running Test cases"){
            steps{
                sh "mvn clean test"
            }
        }

        stage("Maven Build"){
            steps{
                sh "mvn clean install"
            }
        }

        stage('Docker Build Image') {
            steps {
                script{
                    dockerimage=docker.build "madhavsood04/ticketresolver-backend"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script{
                    docker.withRegistry('','DockerHubCred'){
                    dockerimage.push()
                    }
                }
            }
        }

        stage("Removing Image from local machine"){
            steps{
                script{
                    sh 'docker container prune -f'
                    sh 'docker image prune -f'
                }
            }
        }

    }
}
