pipeline {
    agent{
        docker {
            image 'node:alpine'
            args '-e NPM_CONFIG_LOGLEVEL=info'
        }
    }
    stages{
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/dev']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/marius-kengne/tangram.git']]])
            }
        }
        stage('build') {
            steps {
                sh 'sh ./scripts/build.sh'
            }
        }
        stage('test') {
            steps {
                sh 'sh ./scripts/test.sh'
            }
        }        
    }
}