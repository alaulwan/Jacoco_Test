#!groovy
def doneBuild = false

pipeline {
    agent { node { label 'alaa-node' } }

    tools {
        maven 'maven3'
        // jdk 'jdk8'
    }
    stages {
        stage ('Clean') {
            steps {
                sh 'mvn clean'
            }
        }
        stage ('Build') {
            steps {
                sh script {

                    doneBuild = true

                    mvncmd = 'mvn -U install -T 1C'
                    
                    return mvncmd
                }

                }
        }
        stage('Reports') {
            steps {
                jacoco(execPattern: '**/*.exec')
            }
        }
    }
    post {
        always {

            // JUnit Report
            junit allowEmptyResults: !doneBuild, testResults: '**/target/**/*.xml'
        }
    }
}
