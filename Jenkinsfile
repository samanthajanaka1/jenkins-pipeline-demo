pipeline {
    agent any

    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'dev', description: 'Target environment (dev/staging/prod)')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests before deployment?')
        choice(name: 'BUILD_TYPE', choices: ['debug', 'release' , 'optimizedwithdebug'], description: 'Choose the build type')
    }

    environment {
        MY_ENV_VAR = 'HelloJenkins'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo '📥 Cloning repository...'
                echo 'Webhook added'
                git 'https://github.com/octocat/Hello-World.git'
            }
        }

        stage('Build') {
            steps {
                echo "🔨 Building in ${params.BUILD_TYPE} mode..."
                sh 'echo Building the project...'
                sh 'echo $MY_ENV_VAR'
            }
        }

        stage('Test') {
            when {
                expression { return params.RUN_TESTS }
            }
            steps {
                echo '🧪 Running tests...'
                sh 'echo Pretend we are running unit tests here'
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying to ${params.DEPLOY_ENV} environment..."
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
