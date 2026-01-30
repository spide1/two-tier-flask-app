pipeline {
    agent any

    stages {

        stage("code clone") {
            steps {
                echo "Cloning repository"
                git url: "https://github.com/spide1/two-tier-flask-app.git", branch: "master"
                echo "Git clone completed"
            }
        }

        stage("build") {
            steps {
                echo "Build started"
                sh "docker build -t flask-app ."
                echo "Build completed"
            }
        }

        stage("test") {
            steps {
                echo "Running tests"
                // add real test commands here later
                echo "Tests completed"
            }
        }

        stage("push dockerHub") {
    steps {
        withCredentials([usernamePassword(
            credentialsId: "dockerhub-login",
            usernameVariable: "username",
            passwordVariable: "password"
        )]) {
            sh "docker login -u ${env.username} -p ${env.password}"
            sh "docker tag flask-app ${env.username}/flask-app:latest"
            sh "docker push ${env.username}/flask-app:latest"
            echo "Docker push completed"
        }
    }
}


        stage("deploy to server") {
            steps {
                sh """
                    
                    docker compose up -d --build
                    """
            }
        }
    }

    
}
