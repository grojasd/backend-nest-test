pipeline {
    agent any

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