pipeline{
    agent any
    stages{
        stage('Login'){
            steps {
                withCredentials([usernamePassword(credentialsId: 'Cred_for_Dockerhub', usernameVariable : 'USERNAME', passwordVariable : 'PASSWORD')]) {
                    sh 'docker login -u $USERNAME -p $PASSWORD'
            }
        }
    }

    stage('Docker build container nginx'){
        steps {
            dir ('nginx') {
                sh """
                    docker build -t shaytanchik/nginx-laba2:1.${env.BUILD_NUMBER} . 
                    docker push shaytanchik/nginx-laba2:1.${env.BUILD_NUMBER}
                    docker rmi -f shaytanchik/nginx-laba2:1.${env.BUILD_NUMBER}
                """
           }
        }
    }
        
    stage("Docker build container apache"){
        steps {
            dir ('apache') {
                sh """
                    docker build -t shaytanchik/apache-laba2:1.${env.BUILD_NUMBER} .
                    docker push shaytanchik/apache-laba2:1.${env.BUILD_NUMBER}
                    docker rmi -f shaytanchik/apache-laba2:1.${env.BUILD_NUMBER}
                """
                }
            }
        }
    }
}
