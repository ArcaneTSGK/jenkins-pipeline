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
                        def headers = [:]

                        def credentials = "${GIT_USERNAME}:${GIT_PASSWORD}"

                        def encodedCredentials = credentials.bytes.encodeBase64().toString()

                        headers['Authorization'] = "Basic ${encodedCredentials}"

                        def ahead = powershell(returnStatus: true, script: "Invoke-WebRequest -Uri 'https://api.github.com/repos/ArcaneTSGK/jenkins-pipeline/compare/testing...master' -Headers ${headers} | ConvertFrom-Json")
                        echo ahead.status
                    }
                }
            }
        }
    }
}