pipeline {
    agent any  // Runs on any available Jenkins agent
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk'  // Set your Java version here
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }
    stages {
        // Stage 1: Checkout code from GitHub
        stage('Checkout') {
            steps {
                echo 'Checking out the code from GitHub...'
                git branch: 'master', credentialsId: 'github-creds', url: 'https://github.com/HimanshuBafna/POE.git'
            }
        }

        // Stage 2: Build the Java project
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'javac Main.java'  // Compile Java source code (adjust paths if necessary)
            }
        }

        // Stage 3: Test the application (optional)
        stage('Test') {
            steps {
                echo 'Running the Java application...'
                sh 'java Main'  // Running the Main class after compiling (replace with test framework if needed)
            }
        }

        // Stage 4: Dockerize the application (Optional)
        stage('Dockerize') {
            steps {
                echo 'Building the Docker image...'
                script {
                    docker.build('your-image-name')  // This will create the Docker image
                }
            }
        }

        // Stage 5: Push Docker image to Docker Hub (Optional)
        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials-id') {
                        docker.image('your-image-name').push('latest')  // Push the image to Docker Hub
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'This will always run after the pipeline finishes.'
        }
        success {
            echo 'The build was successful!'
        }
        failure {
            echo 'The build failed.'
        }
    }
}
