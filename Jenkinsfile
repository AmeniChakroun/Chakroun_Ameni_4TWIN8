pipeline {

    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {

        stage('Cloner le projet') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AmeniChakroun/Chakroun_Ameni_4TWIN8.git'
            }
        }

        stage('Compilation') {
            steps {
                sh 'mvn clean compile'
            }
        }

    }
}
