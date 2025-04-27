pipeline {
    agent any
    
    environment {
        // Define environment variables
        COMPOSE_FILE = 'docker-compose.yml'
        COMPOSE_PROJECT_NAME = 'laravel-ansible-demo'
        DB_HOST = ${env.DB_HOST}
        DB_PORT = ${env.DB_PORT}
        DB_DATABASE = ${env.DB_DATABASE}
        DB_USERNAME = ${env.DB_USERNAME}
        DB_PASSWORD = ${env.DB_PASSWORD}

    } 

    stages {

        stage('Checkout') {
            steps {
                script {
                    // Clone the repository
                    sh 'echo "Checking out source code..."'
                    checkout scm
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    // Run tests
                    sh 'echo "Running tests..."'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'echo "Building Docker image..."'
                    sh "docker compose -f ${env.COMPOSE_FILE} build"
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container
                    sh 'echo "Running Docker container..."'
                    sh "docker compose -f ${env.COMPOSE_FILE} up -d"
                }
            }
        }
            stage('Run Laravel Migrations') {
            steps {
                script {
                    // Run Laravel migrations
                    sh 'echo "Running Laravel migrations..."'
                    sh "docker compose exec app php artisan migrate --force"
                }
            }
        }
    }

    post {
        success {
            script {
                // Notify success
                sh 'echo "Build and deployment successful!"'
            }
        }
        failure {
            script {
                // Notify failure
                sh 'echo "Build and deployment failed!"'
            }
        }
    }   
}