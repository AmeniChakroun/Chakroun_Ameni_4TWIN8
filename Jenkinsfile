pipeline {
    agent any

    environment {
        // Définit les chemins pour Java et Maven
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        M2_HOME   = '/opt/apache-maven-3.6.3'
        PATH      = "/opt/apache-maven-3.6.3/bin:${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Récupération du code depuis GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compilation du projet...'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Exécution des tests...'
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Création du package...'
                sh 'mvn package -DskipTests'
            }
        }

        stage('Archive Artifacts') {
            steps {
                echo 'Archivage des fichiers jar générés...'
                archiveArtifacts artifacts: '**/target/*.jar', 
                                 fingerprint: true, 
                                 allowEmptyArchive: true
            }
        }
    }

    post {
        always {
            echo 'Pipeline terminé !'
        }
        success {
            echo 'Build réussi et déclenché automatiquement !'
        }
        failure {
            echo 'Le build a échoué. Vérifie les logs !'
        }
    }
}
