pipeline {
    agent any

    environment {
        // On force les bons chemins que tu as déjà
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        M2_HOME   = '/opt/apache-maven-3.6.3'
        PATH      = "/opt/apache-maven-3.6.3/bin:${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn --version'          // juste pour vérifier dans les logs
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }

        stage('Archive') {
            steps {
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
    }
}
