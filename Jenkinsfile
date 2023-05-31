pipeline {

    environment {
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
            }

    agent  any
    stages {
        stage('checkout') {
            steps {
                 script{
                        dir("packer")
                        {
                            git "https://github.com/Shraddhaw4/packerdemo.git"
                        }
                    }
                }
            }
        stage('Validate') {
            steps {
                sh 'pwd;cd packer/ ; packer validate packer.json'
            }
        }
        stage('Build Image') {
            steps {
                sh 'pwd;cd packer/ ; packer validate packer.json'
                }
            }
        }
    }
