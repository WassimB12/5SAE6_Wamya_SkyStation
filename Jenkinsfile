pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                script {
                    // Checkout the code from the specified branch
                    checkout([$class: 'GitSCM', branches: [[name: 'yassineMsadaa5sae6wamya']], userRemoteConfigs: [[url: 'https://github.com/WassimB12/5SAE6_Wamya_SkyStation.git']]])
                }
            }
        }

        stage('Build') {
            steps {
sh "mvn clean install -Dmaven.test.skip=true"            }
        }
 stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv(installationName:'SonarQ') {
                    sh 'mvn sonar:sonar' //  ./chmod +x mvnw  clean org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar
                }
            }
        }
stage('Run Unit Tests with Mockito') {
            steps {
                sh 'mvn test' // Exécutez les tests unitaires avec Mockito en utilisant Maven
                // Utilisez 'gradle test' pour les projets Gradle
            }
        }

        // Add more stages as needed
    }}
