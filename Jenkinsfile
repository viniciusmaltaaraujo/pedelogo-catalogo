pipeline{
    agent any

    stages {
        stage('Checkout Source') {
            steps {
                git url:'git@github.com:viniciusmaltaaraujo/pedelogo-catalogo.git', branch 'main'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    dockerapp = docker.build("viniciusmaltaaraujo/api-produto:${env.BUILD_ID}" , '-f ./src/PedeLogo.Catalogo.Api/DockerFile . ')
                }
            }
        }
        
        stage('Push Image'){
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                    dockerapp.push('latest')
                    dockerapp.push("${env.BUILD_ID}")
                    
                }
            }
        }
        
    }
}