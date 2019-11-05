properties([
	pipelineTriggers([pollSCM('H/3 * * * *')])
	])
node() {
	cleanWs()
	checkout scm
	sh "make"
	sh "./main"
}
node {
    stage('Build') {
        sh 'make'
    }
	stage('Checkout') {
		checkout scm
	}
	stage('Archivage'){
		archiveArtifacts artifacts: 'main', onlyIfSuccessful: true
	}
}
