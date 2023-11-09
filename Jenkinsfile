    pipeline{
    agent any



    stages {


        stage('Getting project from Git') {
            steps{
      			checkout([$class: 'GitSCM', branches: [[name: '*/rim']],
			extensions: [],
			userRemoteConfigs: [[url: 'https://github.com/WassimB12/5SAE6_Wamya_SkyStation.git']]])
            }
        }


       stage('Cleaning the project') {
            steps{
                	sh "mvn -B -DskipTests clean  "
            }
        }



        stage('Artifact Construction') {
            steps{
                	sh "mvn -B -DskipTests package "
            }
        }


/*
         stage('Unit Tests') {
            steps{
               		 sh "mvn test "
            }
        }
*/


        stage('Code Quality Check via SonarQube') {
            steps{

             		sh "mvn clean verify sonar:sonar -Dsonar.projectKey=devops -Dsonar.projectName='devops' -Dsonar.host.url=http://172.10.0.140:9000 -Dsonar.token=sqp_d3624c5a99ade9191b6541c5f376913e6380979c"

            }
        }


        stage('Publish to Nexus') {
            steps {


  sh 'mvn clean package deploy:deploy-file -DgroupId=tn.esprit.spring -DartifactId=gestion-station-ski -Dversion=1.0 -DgeneratePom=true -Dpackaging=jar -DrepositoryId=maven-releases -Durl=http://172.10.0.140:8081/repository/maven-releases/ -Dfile=target/gestion-station-ski-1.0.jar'


            }
        }

stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t rim/spring-app-gl:latest .'
                          }
                      }
                  }

                  stage('login dockerhub') {
                                        steps {
				sh 'docker login -u hajer05 --password dckr_pat_RSXhVF95RdTy-kosv9b4ocrP5AI'
                                            }
		  }

	                      stage('Push Docker Image') {
                                        steps {
                                   sh 'docker push hajer05/spring-app-twin:latest'
                                            }
		  }


		   stage('Run Spring && MySQL Containers') {
                                steps {
                                    script {
                                      sh 'docker compose up -d'
                                    }
                                }
                            }






}


        post {
		/*success{
		mail bcc: '', body: '''Dear Mr,
we are happy to inform you that your pipeline build was successful.
Great work !
-Jenkins Team-''', cc: '', from: 'rim.mabrouki@esprit.tn', replyTo: '', subject: 'Build Finished - Success', to: 'rim.mabrouki@esprit.tn'
		}

		failure{
mail bcc: '', body: '''Dear mr,
we are sorry to inform you that your pipeline build failed.
Keep working !
-Jenkins Team-''', cc: '', from: 'rim.mabrouki@esprit.tn', replyTo: '', subject: 'Build Finished - Failure', to: 'rim.mabrouki@esprit.tn'
		}*/

       always {
		//emailext attachLog: true, body: '', subject: 'Build finished',from: 'rim.mabrouki@esprit.tn' , to: 'rim.mabrouki@esprit.tn'
            cleanWs()
       }
    }



}

