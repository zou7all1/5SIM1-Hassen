pipeline {
    agent any

    tools {
        maven 'M2_HOME'
        jdk 'JAVA_HOME'
    }

    stages {
        stage('Build Backend') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    dir('backend') {
                        // Explicitly use the Maven tool
                        def mvnHome = tool 'M2_HOME'
                        sh "${mvnHome}/bin/mvn sonar:sonar -Dsonar.projectKey=DevOps-AppGestionDesProjets -Dsonar.projectName=DevOps-AppGestionDesProjets -Dsonar.sources=src"
                    }
                }
            }
        }
    }
}
