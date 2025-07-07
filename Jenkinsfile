pipeline {
    agent any
    environment {
        NPM_CONFIG_CACHE= "${WORKSPACE}/.npm" 
        dockerImagePrefix = "us-west1-docker.pkg.dev/lab-agibiz/docker-repository"
        registry = "https://us-west1-docker.pkg.dev"
        registryCredentials = 'gcp-registry'
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
            
                stage ("Ejecucion de pruebas"){
                    steps {
                        sh 'npm run test:cov'
                    }
                }

                stage ("Construccion de la aplicacion"){
                    steps {
                        sh 'npm run build'
                    }
                }
            }
        }
        stage ("Crear imagen docker") {
            steps {
                script {
                    docker.withRegistry("${registry}", registryCredentials){
                        sh "docker build -t backend-nest-test-grd ."
                        sh "docker tag backend-nest-test-grd ${dockerImagePrefix}/backend-nest-test-grd"
                        sh "docker push ${dockerImagePrefix}/backend-nest-test-grd"
                    }
                }
            }
            
        }
    }
}