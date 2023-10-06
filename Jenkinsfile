node {
    docker.image('node:lts-buster-slim').inside('-p 3000:3000') {
        withEnv(['CI = true']) {
            stage('Build') {
                sh 'npm install'
            }
            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
            stage('Manual Approval') {
                input message: 'Lanjutkan ke tahap Deploy?'
            }
                stage('Deploy') {
                sh './jenkins/scripts/deliver.sh'
                sleep(time: 1, unit: 'MINUTES')
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}