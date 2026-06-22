@Library("Shared") _

pipeline {
    agent {
        label "agent1"
    }

    stages {

        stage("Code Fetch") {
            steps {
                script {
                    clone(
                        "https://github.com/shamelsk/node-to-do-app.git",
                        "main"
                    )
                    echo "Fetched Code Successfully"
                }
            }
        }

        stage("Code Build") {
            steps {
                script {
                    docker_build(
                        imageName: "node-to-do-app"
                    )
                }
            }
        }

        stage("Code Test") {
            steps {
                echo "Testing Code"
            }
        }

        stage("Push to DockerHub") {
            steps {
                docker_push(
                    sourceImage: "node-to-do-app",
                    imageName: "shamel1012/node-to-do-app",
                    credentialsId: "dockerHubCred"
                )
            }
        }

        stage("Code Deploy") {
            steps {
                echo "Deploying Code"
                sh "docker compose down"
                sh "docker compose up -d"
            }
        }

    }
}
