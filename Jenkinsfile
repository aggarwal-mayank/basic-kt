// Uses Declarative syntax to run commands inside a container.
pipeline {
    agent {
        kubernetes {
            yamlFile 'jenkins-pod.yaml'
        }
    }
    environment {
        GCR_PASS= credentials('gcrPass')
    }
    stages {
        // stage('Test') {
        //     steps {
        //         container('gradle') {
        //             sh 'pwd'
        //             sh 'gradle test'
        //             sh 'ls -alh'
        //         }
        //     }
        // }

        // stage('Build') {
        //     steps {
        //         container('gradle') {
        //             sh 'pwd'
        //             sh 'gradle bootJar'
        //             sh 'ls -alh'
        //         }
        //     }
        // }

        stage('Publish') {
            steps {
                container('gradle') {
                    sh 'gradle task --all'
                    //sh 'gradle --stacktrace jib --image=gcr.io/practicek8s/basic-kt:latest'
                    sh 'gradle jib -PgcrUser=_json_key -PgcrPass=$GCR_PASS'
                    sh 'ls -alh'
                }
            }
        }
    }
}
