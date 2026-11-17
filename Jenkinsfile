pipeline {
    agent any

    environment {
        PATH = "/usr/local/share/dotnet:${env.PATH}"
    }

    stages {
        stage('Verify Main Branch') {
            steps {
                script {
                    if (env.GIT_BRANCH != 'origin/main' && env.GIT_BRANCH != 'main') {
                        error("Pipeline is allowed only on main. Current branch: ${env.GIT_BRANCH}")
                    }
                }
            }
        }

        stage('Restore') {
            steps {
                sh 'dotnet restore Homies.sln'
            }
        }

        stage('Build') {
            steps {
                sh 'dotnet build Homies.sln --no-restore'
            }
        }

        stage('Test') {
            steps {
                sh 'dotnet test Homies.sln --no-build'
            }
        }
    }
}
