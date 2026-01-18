pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                cd /var/lib/jenkins/workspace/jenkins-ci-demo

                echo "Stopping old app..."
                pm2 delete jenkins-ci-demo || true

                echo "Starting app with PM2..."
                pm2 start server.js --name jenkins-ci-demo

                pm2 save

                pm2 list
                '''
            }
        }
    }
}
