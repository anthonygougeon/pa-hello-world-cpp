properties([
	pipelineTriggers([pollSCM('H/3 * * * *')])
	])
node() {
	cleanWs()
	checkout scm
	sh "make"
	sh "./main"
}
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh './main build'
            }
        }
        stage('Test') {
            steps {
                sh './main check'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'build/libs/**/*.jar', fingerprint: true
            junit 'build/reports/**/*.xml'
        }
    }
}
