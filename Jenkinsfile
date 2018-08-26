@Library('jenkins-shared-library@master') _

pipeline {
    agent { dockerfile true }

    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        timestamps()
        ansiColor('xterm')
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {
        stage('Prepare') {
            steps { script {
                currentBuild.description = "commit: ${git.shortCommit}, last author: ${git.authorName}"
            }}
        }

        stage('Build') {
            steps { script {
                xgradle.build()
            }}

            post {
                always { script {
                    xgradle.publish()
                }}
            }
        }
    }
}
