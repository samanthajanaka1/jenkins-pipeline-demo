pipeline {
    agent any

    environment {
        MY_ENV_VAR = 'HelloJenkins'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo '📥 Cloning repository...'
                echo ' webhook added'
                git 'https://github.com/octocat/Hello-World.git'
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Building...'
                sh 'echo Building the project...'
                sh 'echo $MY_ENV_VAR'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh 'echo Pretend we are running unit tests here'
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Deploying...XXXXX'
                sh 'echo Deployment simulated'
            }
        }
    }

    post {
        always {
            echo '✅ Pipeline complete (success or fail)'
        }
        success {
            echo '🎉 Build was successful!'
        }
        failure {
            echo '💥 Build failed!'
        }
    }
}
