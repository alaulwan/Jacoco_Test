#!groovy
def call() {

    def doneBuild = false

    pipeline {

        agent {
            label 'artifactory-single'
        }
        tools {
            maven 'maven3'
            jdk 'jdk8'
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
        }
        post {
            always {

                // JUnit Report
                junit allowEmptyResults: !doneBuild, testResults: '**/target/**/*.xml'

                cleanWs(
                    deleteDirs: true,
                    notFailBuild: true,
                    patterns: [
                        [pattern: 'build', type: 'INCLUDE'],
                        [pattern: 'target', type: 'INCLUDE']
                    ]
                )
            }
        }
    }
}
