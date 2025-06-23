pipeline {

    agent any

    environment {
        CHROME_VERSION = "137.0.7151.120"
        CHROMEDRIVER_VERSION = "137.0.7151.11900"
        CHROME_INSTALL_PATH = "C:\\Program Files\\Google\\Chrome\\Application"
        CHROMEDRIVER_PATH = "C:\\Program Files\\Google\\Chrome\\Application\\chromedriver.exe"
    }

    stages {
        stage("Checkout code") {
            steps {
                checkout scm        
            }
        }

        stage("Set up .NET Core") {
            steps {
                bat "choco install dotnet-sdk -y --version=6.0.100"  
            }
        }

        stage("Restore dependencies") {
            steps {
                bat "dotnet restore"
            }
        }

        stage("Build") {
            steps {
                bat "dotnet build --configuration Release"
            }
        }

        stage("Run tests") {
            steps {
                bat "dotnet test"
            }
        }
    }

    post {
       success {
            echo "Build sucessful"
        }

        failure {
            echo "Build failed"
        }

        aborted {
            echo "Build aborted"
        }

        unstable {
            echo "Tests failed"
        }

    }

}