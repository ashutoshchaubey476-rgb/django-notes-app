@Library('shared') _
pipeline {

    agent { label 'vinod' }

    triggers {
        githubPush()
    }

    stages {

        stage("hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage("Code") {
            steps {
                script {
                    clone("https://github.com/ashutoshchaubey476-rgb/django-notes-app.git", "main")
                }
            }
        }

        stage("Build") {
            steps {
                script {
                    docker_build("notes-app", "latest", "ashutosh476")
                }
            }
        }

        stage("Push to DockerHub") {
            steps {
                script {
                    docker_push("notes-app", "latest", "ashutosh476")
                }
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying application using Docker Compose"
                //sh "docker compose down || true"
                sh "docker compose up -d"
            }
        }

    }
}
