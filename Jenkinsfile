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
                sh './gradlew build'
            }
        }
        stage('Test') {
            steps {
                sh './gradlew check'
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
