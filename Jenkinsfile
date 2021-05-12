pipeline {
    agent any
    triggers {
        pollSCM('* * * * *')
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deployments') {
            parallel {
                stage('Deploy to Staging') {
                    steps {
                        sh "cp /c/Windows/system32/config/systemprofile/AppData/Local/Jenkins/.jenkins/workspace/fully-automated-pipeline/target/parallel-stages.war /d/development/servers/apache-tomcat-9.0.38-staging/webapps"
                    }
                }
                stage('Deploy to Production') {
                    steps {
                        sh "cp /c/Windows/system32/config/systemprofile/AppData/Local/Jenkins/.jenkins/workspace/fully-automated-pipeline/target/parallel-stages.war /d/development/servers/apache-tomcat-9.0.38-prod/webapps"
                    }
                }
            }
        }
    }
}