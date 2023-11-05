pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh "mvn clean package -DskipTests"
            }
        }
        
        stage('Docker Build') { 
            steps { 
                script{
                 app = docker.build("msadaayessine_wamya_skystation")
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Assuming SonarQube is running on http://localhost:9000
                    withSonarQubeEnv(installationName: 'sonarqube') {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }

        stage('Run Unit Tests with Mockito') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
