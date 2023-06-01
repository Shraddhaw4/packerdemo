pipeline {

    // environment {
    //     AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
    //     AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    //         }

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
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID', // dev credentials
                    credentialsId: 'AWS_CREDS',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                    ]])
                { sh 'pwd;cd packer/ ; packer validate packer.json' }
            }
        }
        stage('Build Image') {
             steps {
                 withCredentials([[
                 $class: 'AmazonWebServicesCredentialsBinding',
                 accessKeyVariable: 'AWS_ACCESS_KEY_ID', // dev credentials
                 credentialsId: 'AWS_CREDS',
                 secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                 ]]){
                       sh 'pwd;cd packer/ ;packer build packer.json'
                    }
                 }
             }
        }
    }
