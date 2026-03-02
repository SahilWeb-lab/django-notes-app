@Library("Shared") _
pipeline {
    agent any 
    
    stages {
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }
        stage("Code") {
            steps {
                script {
                    clone("https://github.com/SahilWeb-lab/django-notes-app.git", "dev")
                }
            }
        }
        stage("Build") {
            steps {
                script {
                    docker_build("sahilmandal", "notes-app", "latest")
                }
            }
        }
        stage("Push image to docker hub") {
            steps {
                script {
                    docker_push("notes-app", "latest")
                }
            }
        }
        stage("Deploy") {
            steps {
                echo "Deploying started..."
                // sh "docker run -d -p 8000:8000 notes-app:latest"
                sh "docker compose up -d"
                echo "Delploying finished..."
            }
        }
    }
}
