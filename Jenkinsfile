pipeline {

    // environment {
    //     AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
    //     AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY')
    //         }

    agent {label 'packer'}
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
     //             accessKeyVariable: 'AWS_ACCESS_KEY_ID', // dev credentials
                    credentialsId: 'AWS_credentials',
     //             secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                    ]])
                { sh 'pwd;cd packer/ ; packer validate packer.json' }
            }
        }
        stage('Build Image') {
             steps {
                 withCredentials([[
                 $class: 'AmazonWebServicesCredentialsBinding',
                 accessKeyVariable: 'AWS_ACCESS_KEY_ID', // dev credentials
                 credentialsId: 'AWS_credentials',
                 secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                 ]]){
                       sh 'pwd;cd packer/ ;packer build packer.json'
                    }
                 }
             }
        }
    }
