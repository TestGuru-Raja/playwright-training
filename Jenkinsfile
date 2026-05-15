pipeline {
    agent any

    tools {
        nodejs "Node18"
    }

    stages {

        stage('Checkout') {
    steps {
        checkout([$class: 'GitSCM',
            branches: [[name: '*/main']],
            userRemoteConfigs: [[url: 'https://github.com/TestGuru-Raja/playwright-training.git']]
        ])
    }
}


        stage('Install Dependencies') {
            steps {
                bat 'echo Installing npm packages...'
                bat '"%NODEJS_HOME%\\npm.cmd" install'
            }
        }

        stage('Install Playwright Browsers') {
            steps {
                bat '"%NODEJS_HOME%\\npx.cmd" playwright install'
            }
        }

        stage('Run Playwright Tests') {
            steps {
                bat '"%NODEJS_HOME%\\npx.cmd" playwright test --reporter=html'
            }
        }

        stage('Archive Reports') {
            steps {
                archiveArtifacts artifacts: 'playwright-report/**'
            }
        }
    }
}
