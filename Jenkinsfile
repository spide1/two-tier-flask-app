pipeline
{
    agent any

    stages{
        stage("code clone"){
            steps{
                sh "git to clone "
                git url: "https://github.com/spide1/two-tier-flask-app.git", branch: "master"
                sh "git clone completed"
            }
        }
        stage("build"){
            steps{
                sh "echo build started"
                sh "docker build -t flask-app ."
                sh "echo build completed"
            }
        }
        stage("test"){
            steps{
                sh "test code"
                sh "test completed"
            }
        }
        stage("push dockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId: "dockerhub-login",
                    usernameVariable: "username",
                    passwordVariable: "password"
                    sh "docker login -u ${env.username} -p ${env.password}"
                    sh "docker tag flask-app ${env.username}/flask-app:latest"
                    sh "docker push ${env.username}/flask-app:latest"
                    sh "docker push completed"
                )])
            }
        }
        stage("deploy to server"){
            steps{
                sh "docker compose down && docker compose up -d --build"

            }
        }
        post{
            success{
                sh "echo Pipeline succeeded!"
            }
            failure{
                sh "echo Pipeline failed!"
        }
    }
}
