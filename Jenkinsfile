@Library("Shared") _
pipeline {
    agent { label "vinod" }
    
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
                    docker_build("sahilmandal","notes-app", "latest")
                }
            }
        }
        stage("Push to docker hub") {
          steps {
              script {
                  docker_push("notes-app", "latest")
              }
              echo "Pushing finshed to docker hub."
          }
        }
        stage("Deploy") {
            steps {
                echo "Code deploying start."
                // sh "docker run -d -p 8000:8000 notes-app:latest"
                sh "docker compose down && docker compose up -d"
                echo "Code deploying finish."
            }
        }
    }
}
