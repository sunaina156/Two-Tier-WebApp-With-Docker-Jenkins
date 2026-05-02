pipeline {
    agent any

    stages {

        stage("Clone Code") {
            steps {
                git branch: 'main', url: 'https://github.com/sunaina156/Two-Tier-WebApp-With-Docker-Jenkins.git'
            }
        }

        stage("Build Docker Image") {
            steps {
                sh "docker build -t two-tier-flask-app ."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerHubCreds',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS')]) {

                    sh """
                    echo $PASS | docker login -u $USER --password-stdin
                    docker tag two-tier-flask-app $USER/two-tier-flask-app
                    docker push $USER/two-tier-flask-app
                    """
                }
            }
        }

        stage("Deploy") {
            steps {
                sh "docker compose up -d --build"
            }
        }
    }

    post {
        success {
            echo "Build Successful"
        }
        failure {
            echo "Build Failed"
        }
    }
}