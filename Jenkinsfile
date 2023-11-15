pipeline {
    agent any
    environment {
       		DOCKERHUB_CREDENTIALS=credentials('id')
       	}


    stages {
        stage('Récupération du code') {
            steps {
                checkout scm
            }
        }

        stage('Lancement de la commande Maven') {
            steps {
                sh 'mvn clean compile'
            }
        }
        stage('SonarQube Scan') {
            steps {
                sh 'mvn sonar:sonar -Dsonar.login=squ_2df466b398f9bc76f19c6f590f1bee878dd26203'
            }
        }
         stage("mockito"){
                            steps {
                                sh 'mvn -Dtest=mockito test'
                            }
                        }

               stage('mvn deploy'){
                    steps {
                        sh "mvn deploy"
                    }
               }
                stage('Docker Image') {
                                  steps {
                                      sh 'sudo docker build -t syrinebenslim-5nids2-g2 .'
                                  }
                      }

                       stage('DOCKERHUB') {
                                         steps {
                                             sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                                             sh 'docker tag syrinebenslim-5nids2-g2  syrinebs/syrinebenslim-5nids2-g2:1.0.0'
                                             sh 'docker push syrinebs/syrinebenslim-5nids2-g2:1.0.0'
                                         }
                                     }


                      stage('Docker Compose') {
                                  steps {
                                      sh 'docker compose up -d'
                                  }
                      }
                      stage('Junit') {
                                  steps {
                                      sh 'mvn -Dtest=Junit test'
                                  }
                              }
                              






}

}



