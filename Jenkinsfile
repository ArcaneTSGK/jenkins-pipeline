#!/usr/bin/env groovy

pipeline {
    agent any
    options {
        skipDefaultCheckout()
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Branch Analysis') {
            steps {
                withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'git-credentials', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {
                    script {
                        def credentials = "${GIT_USERNAME}:${GIT_PASSWORD}"
                        def encodedCreds = credentials.bytes.encodeBase64().toString()

                        def ahead = powershell(returnStatus: true, script: "Invoke-WebRequest -Uri 'https://api.github.com/repos/ArcaneTSGK/jenkins-pipeline/compare/testing...master' -Headers @{'Authorization' = 'Basic $encodedCreds'} | ConvertFrom-Json")
                        echo ahead
                    }
                }
            }
        }
    }
}