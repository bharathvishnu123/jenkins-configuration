pipeline {
    agent any

    environment {
        MAVEN_HOME = tool name: 'Maven 3', type: 'maven'
        JAVA_HOME  = tool name: 'JDK 17', type: 'jdk'
        PATH       = "${MAVEN_HOME}/bin:${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bharathvishnu123/jenkins-configuration.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Verify Build') {
            steps {
                sh 'mvn verify'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy (Optional)') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying artifact...'
                // sh 'mvn deploy'
            }
        }
    }

    post {
        success {
            echo 'Build, verification, and artifact archiving succeeded!'
        }
        failure {
            echo 'Build failed. Check console output for details.'
        }
    }
}
