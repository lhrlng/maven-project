pipeline {
    agent any

    parameters {
        string(name: 'tomcat_dev', defaultValue: '127.0.0.1:7070', description: 'Staging Server')
        string(name: 'tomcat_prod', defaultValue: '127.0.0.1:9090', description: 'Production Server')
    }

    triggers {
        pollSCM('* * * * *')
    }

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

        stage('Deployments'){
            parallel{
                stage('Deploy to Staging'){
                    steps{
                        sh "cp http://localhost:8182/job/FullyAutomated/lastSuccessfulBuild/artifact/webapp/target//webapp.war ${tomcat_dev}"
                    }
                }
                stage('Deploy to Production'){
                    steps{
                        sh "cp **/target/*.war ${tomcat_prod}"
                    }
                }
            }
        }
    }
}