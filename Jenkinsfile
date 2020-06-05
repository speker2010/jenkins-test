pipeline {
    agent none

    stages {
        stage('Build') {
            agent{
                docker { 
                    image 'composer:2.0'
                    args '--volume $HOME:/app'
                }
            }
            steps {
                sh 'composer install'
            }
        }
        stage('Test') {
            agent {
                docker {
                    image 'php:7.3-cli'
                    args '-v "$HOME":/usr/src/myapp -w /usr/src/myapp'
                }
            }
            steps {
                sh './vendor/bin/phpunit tests --log-junit builds/tests/result.xml'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }

    post {
        always {
            junit 'build/tests/result.xml'
        }
    }
}