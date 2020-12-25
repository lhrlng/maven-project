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
                        sh "cp -i **/target/*.war ${params.tomcat_dev}/C:\tomcat-multiple-instances\instance-1\webapps"
                    }
                }
                stage('Deploy to Production'){
                    steps{
                        sh "cp -i **/target/*.war ${params.tomcat_prod}/C:\tomcat-multiple-instances\instance-1\webapps"
                    }
                }
            }
        }
    }
}