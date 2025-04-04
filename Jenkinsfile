pipeline {
    agent any

    parameters {
        string(name: 'APP_VERSION', defaultValue: '1.0.0', description: 'Application version')
        choice(name: 'DEPLOY_ENV', choices: ['dev', 'staging', 'prod'], description: 'Target environment')
        booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run test suite?')
    }

    environment {
        ARTIFACT_DIR = "artifacts"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo ' Cloning repository...'
                git 'https://github.com/octocat/Hello-World.git'
            }
        }

        stage('Build') {
            steps {
                echo " Building app version ${params.APP_VERSION}..."
                sh '''
                    mkdir -p ${ARTIFACT_DIR}
                    echo "Build for version ${APP_VERSION}" > ${ARTIFACT_DIR}/build.log
                '''
            }
        }

        stage('Run Tests') {
            when {
                expression { return params.RUN_TESTS }
            }
            steps {
                echo ' Running tests...'
                sh '''
                    echo "Tests passed!" > ${ARTIFACT_DIR}/test-results.log
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.DEPLOY_ENV} environment..."
                sh 'sleep 2'
                sh "echo Deployed version ${params.APP_VERSION} to ${params.DEPLOY_ENV} > ${ARTIFACT_DIR}/deploy.log"
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: "${ARTIFACT_DIR}/*.log", fingerprint: true
            }
        }
    }

    post {
        success {
            echo ' Build finished successfully!'
        }
        failure {
            echo 'Build failed.'
        }
    }
}
