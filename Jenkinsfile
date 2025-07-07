pipeline {
    agent any
    environment {
        NPM_CONFIG_CACHE= "${WORKSPACE}/.npm" 
    }

    stages {
        stage ("Proceso de build y test") {
            agent {
                docker {
                    image 'node:22'
                    reuseNode true
                }
            }
            stages {
                stage ("Instalacion de dependencias"){
                    steps {
                        sh 'npm ci'
                    }
                }
            }
            
        }
    }
}