pipeline {
    agent any

    environment {
        DOTNET_VERSION = '6.0.x'
    }

    stages {
        stage('Checkout the repo') {
            steps {
                checkout scm
            }
        }
        stage('Setup .NET') {
            steps {
                sh '''
                    if ! dotnet --list-sdks | grep 6.0; then
                        wget https://dot.net/v1/dotnet-install.sh -O dotnet-install.sh
                        chmod +x dotnet-install.sh
                        ./dotnet-install.sh --version 6.0.100
                        export PATH=$PATH:~/.dotnet
                    fi
                '''
            }
        }
        stage('Restore dependencies') {
            steps {
                sh 'dotnet restore'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build --no-restore'
            }
        }
        stage('Test') {
            steps {
                sh 'dotnet test --no-build --verbosity normal'
            }
        }
    }
}
