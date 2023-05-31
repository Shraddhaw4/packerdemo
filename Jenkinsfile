pipeline {
    agent  any

    stages {
        stage('Build Image') {
            environment {
                AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
                AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
            }
            steps {
                withCredentials([string(credentialsId: 'AWS_ACCESS_KEY_ID', variable: 'AWS_ACCESS_KEY_ID'),
                                 string(credentialsId: 'AWS_SECRET_ACCESS_KEY', variable: 'AWS_SECRET_ACCESS_KEY')]) {
                    
                        // Run Packer build command
                        sh 'packer build -var access_key=${AWS_ACCESS_KEY_ID} -var secret_key=${AWS_SECRET_ACCESS_KEY} packer.json')
                }
            }
        }
    }
}
