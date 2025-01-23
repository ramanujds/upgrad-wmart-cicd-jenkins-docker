pipeline {
    agent any

    tools {

        maven "maven-3.9.9"
    }

    stages {
        stage('Source') {
            steps {
                // Get some code from a GitHub repository
                checkout scmGit(branches: [[name: '*/main']], extensions: [],
                        userRemoteConfigs: [[credentialsId: 'github-credentials',
                                               url: 'https://github.com/ramanujds/upgrad-wmart-cicd-jenkins-docker.git']])

            }
         }

         stage('Test'){
            steps{
                sh "mvn test"
                echo 'Test Success'
            }
         }

        stage('Build Jar'){
            steps{
                    sh "mvn clean package"
                    echo 'Build Success'
                }
            }

        stage('Build Docker Image'){
            steps{
                sh "docker build -t ram1uj/spring-boot-app-wmart ."
                echo 'Docker Image Build Success'
            }
        }

        }


        post{
         success{
            junit '**/target/surefire-reports/TEST-*.xml'
            archiveArtifacts 'target/*.jar'
            echo 'Build Complete'
          }
        }

}