@Library("Shared") _
pipeline {
    
    agent { label "agent-1" }
    
    stages {
        
        stage("Shared Library") {
            steps {
                script {
                    demo()
                }
            }
        }
        
        stage('Code') {
            steps {
                script {
                    clone("https://github.com/SahilWeb-lab/django-notes-app.git", "dev")
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    docker_build("sahilmandal","notes-app", "latest")
                }
            }
        }
        
        stage('Push to Dockerhub') {
            steps {
                script {
                    docker_push("notes-app", "latest")
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    docker_compose()
                }
                sh "docker compose down && docker compose up -d"
            }
        }
        
    }
    
}
