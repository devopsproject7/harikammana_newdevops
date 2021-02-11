pipeline {
    agent any
    tools {
        maven 'maven-3'
    }
    options {
        buildDiscarder logRotator(daysToKeepStr: '5', numToKeepStr: '7')
    }
    stages{
        stage('Build'){
            steps{
                 sh script: 'mvn clean package'
                 archiveArtifacts artifacts: 'target/*.war', onlyIfSuccessful: true
            }
        }
        stage('Upload War To Nexus'){
            steps{
                script{
nexusArtifactUploader artifacts: [[artifactId: 'simple-app', classifier: '', file: 'target/simple-app-3.0.0-SNAPSHOT', type: 'war']], credentialsId: 'nexus3', groupId: 'in.javahome', nexusUrl: '172.31.68.19', nexusVersion: 'nexus2', protocol: 'http', repository: 'http://ec2-34-204-206-47.compute-1.amazonaws.com:8081/repository/simpleapp-release/', version: '3.0.0-SNAPSHOT'
                    }
            }
        }
    }
}
