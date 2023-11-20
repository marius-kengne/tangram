pipeline {
    agent{
        docker {
            image 'node:alpine'
            args '-e NPM_CONFIG_LOGLEVEL=info -p 8000:8000'
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
        stage('validate') {
            steps {
                input message:'Validation manuelle (voir tâche suivante)', ok:'Allons-y'
                sh 'sh ./scripts/validate.sh 8000'
            }
        }
        stage('deploy') {
            steps {
                archiveArtifacts artifacts: 'out/*', fingerprint: true
                sh 'sh ./scripts/deploy.sh'
            }
        }     
    }
}