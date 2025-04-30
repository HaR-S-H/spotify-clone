node {
    stage('Checkout') {
        git 'https://github.com/HaR-S-H/spotify-clone.git'
    }

    stage('Build') {
        sh 'npm install'
    }

    stage('Test') {
        sh 'npm test'
    }

    stage('Deploy') {
        sshPublisher(publishers: [
            sshPublisherDesc(
                configName: 'production-server',
                transfers: [
                    sshTransfer(
                        sourceFiles: 'dist/**',
                        removePrefix: 'dist',
                        remoteDirectory: '/var/www/app'
                    )
                ],
                execCommand: 'pm2 restart app'
            )
        ])
    }
}
