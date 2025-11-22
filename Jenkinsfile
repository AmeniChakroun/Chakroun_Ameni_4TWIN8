pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh './mvnw clean compile'          // ← ./mvnw au lieu de mvn
            }
        }

        stage('Test') {
            steps {
                sh './mvnw test'                   // ← ./mvnw
            }
        }

        stage('Package') {
            steps {
                sh './mvnw package -DskipTests'    // ← ./mvnw
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true, allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo "Pipeline terminé"
        }
    }
}
