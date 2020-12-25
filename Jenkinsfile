pipeline {
    agent any
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success{
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Bla1'){
            steps {
                echo 'Bla1...'
            }
        }
        stage('Bla2'){
            steps {
                echo 'Code Bla2.'
            }
        }
    }
}