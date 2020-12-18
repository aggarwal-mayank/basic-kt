// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            yamlFile 'jenkins-pod.yaml'
        }
    }
    environment {
        GCP_SA = credentials('gcp-sa')
    }
    stages {
        stage('Test') {
            steps {
                container('gradle') {
                    sh 'pwd'
                    sh 'gradle test'
                    sh 'ls -alh'
                }
            }
        }

        stage('Build') {
            steps {
                container('gradle') {
                    sh 'pwd'
                    sh 'gradle bootJar'
                    sh 'ls -alh'
                }
            }
        }

        stage('Publish') {
            steps {
                container('gradle') {
                    sh 'pwd'
                    sh 'gradle jib -Djib.to.image=gcr.io/practicek8s/basic-kt:latest -Djib.to.auth.username=$GCP_SA_USR -Djib.to.auth.password=$GCP_SA_PSW'
                    sh 'ls -alh'
                }
            }
        }
    }
}
