pipeline {
    agent any



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





}

}



