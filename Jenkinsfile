pipeline {
    agent any
    
    triggers {
        pollSCM('H/15 * * * *')
    }

    stages {
        stage('Identificación') {
            steps {
                sh 'echo "CD ejecutado por: Karol (eim-alu-69005)"'
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kbayona-r/Testing-React-Redux-with-Jest-and-Enzyme.git'
            }
        }

        stage('Build y Test (Node 14)') {
            steps {
                script {
                    docker.image('node:14-bullseye').inside {
                        sh '''
                            apt-get update
                            apt-get install -y python make g++ build-essential libc6-dev
                            npm install --legacy-peer-deps
                            npm run build
                            npm test
                        '''
                    }
                }
            }
        }
        stage('Deploy en Escritorio del host') {
            steps {
                sh '''
                    mkdir -p /home/alumno/Escritorio/despliegue
                    cp -r README.md Utils build node_modules package*.json public src yarn.lock \
                        /home/alumno/Escritorio/despliegue/ 2>/dev/null
                '''
            }
        }

        stage('Deploy en contenedor Docker interno') {
            steps {
                sh '''
                    docker build -t proyecto-react .
                    docker run -d --name contenedor-react -p 3000:3000 proyecto-react \
                
                '''
            }
        }
    }

    post {
        always {
            sh 'rm -rf node_modules || true'
            sh 'npm cache clean --force || true'
        }
    }
}
