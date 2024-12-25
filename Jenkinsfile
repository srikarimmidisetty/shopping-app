pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'Maven 3.8.7', type: 'maven' // Adjust the Maven tool name if needed
        JAVA_HOME = tool name: 'JDK 17', type: 'jdk'        // Ensure Java 17 is configured
        PATH = "${MAVEN_HOME}/bin:${PATH}"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Set Up Environment') {
            steps {
                echo 'Setting up environment...'
                sh 'mvn -version'
            }
        }

        stage('Compile') {
            steps {
                echo 'Compiling the code...'
                sh 'mvn clean compile'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('Package Application') {
            steps {
                echo 'Packaging the application...'
                sh 'mvn package'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archiving the built artifacts...'
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running the application...'
                sh 'java -jar target/shopping-app-0.0.1-SNAPSHOT.jar'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment completed successfully.'
        }
        failure {
            echo 'Build failed. Please check the logs for errors.'
        }
    }
}
