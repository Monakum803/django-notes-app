@Library("Shared") _
pipeline {
    agent { label "Bhupendra" }

    stages {
        stage ("Hello") {
            steps {
                script {
                    hello()
                }
            } 
        }
        
        stage('Code Clone') {
            steps {
                script {
                    echo "Starting code clone..."
                    clone("https://github.com/Monakum803/django-notes-app.git", "main")
                    echo "Code clone completed."
                }
            }    
        }
        
        stage('Build') {
            steps {
                script {
                    echo "the code building starting by docker"
                    docker_build("notes-app", "latest", "bhupendradixit")   
                }
            }
        }
        
        stage('Code Pull') {
            steps {
                echo 'The code is pulling stage'
            }
        }

        stage('Code Push on Docker Hub') {
            steps {
                script {
                    docker_push("notes-app", "latest", "bhupendradixit")
                }
            }
        }
        
        stage('Code Deploy') {
            steps {
                echo 'The code is deploying'
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
