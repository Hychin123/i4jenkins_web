pipeline {
    agent any // windows agent, Jenkins-Laravel (other machine)
    environment {
        BOT_TOKEN = '6587888932:AAEm5NBhKAV9kYPWdBaKaRbZa2YDRKEoHiM'
        CHAT_ID = '-1002015349324'
    }
    stages {
        stage('Fetch from GitHub') { // build steps
            steps {
                echo 'Fetching from GitHub'
                git branch: 'Tp03', url:'https://github.com/Hychin123/i4jenkins_web.git'
            }
        }
        stage('Build using Tools') {
            steps {
                echo 'Compiling code...'
                sh 'cp .env.example .env'
                sh 'composer install && php artisan key:generate && npm install && npm run build'
            }
        }
        stage('Test the app') {
            steps {
                echo 'Testing unit tests...'
                echo 'Testing features...'
                sh 'php artisan test'
            }
        }
    }
    post {
        success {
            sh '''
                bash scripts/deployment.sh SUCCESS🟢
            '''
        }
        failure {
            sh '''
                bash scripts/deployment.sh FAILED🔴
            '''
        }
    }
}

