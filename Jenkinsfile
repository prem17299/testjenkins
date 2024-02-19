pipeline {

    agent any

    tools {

        maven "maven_home"

    }

    stages {

        stage('Checkout'){

            steps{

                git branch: 'main', url: 'https://github.com/prem17299/testjenkins.git'

            }

        }

        stage('Clean'){

            steps{

                bat "mvn clean"

            }

        }

        stage('Build and Test') {

            steps {

                bat "mvn -Dmaven.test.failure.ignore=true package"

            }

            post {

                success {

                    junit '**/target/surefire-reports/TEST-*.xml'

                    archiveArtifacts 'target/*.jar'

                }

            }

        }

        stage('Build Docker Image'){

            steps{

                script{

                    bat "docker build -t jenkinsassignment3 -f Dockerfile ."

                }

            }

        }

        stage('Run Docker Image'){

            steps{

                script{

                    bat "docker run jenkinsassignment3."

                }

            }

        }

    }

}
