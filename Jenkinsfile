pipeline {
    agent any
    
    environment {
        branchName = Version.tokenize('/').last() //'refs/heads/main'
    }


    stages {

        
        stage('login to dockerhub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'docker_username', passwordVariable: 'docker_password')]) {
                        sh "docker login https://index.docker.io/v1/ --username \"\$docker_username\" --password \"\$docker_password\""
                    }                    
                }
            }
        }

        stage('Build and Publish BE') {
            steps {
                script {
                        sh '''
                        image_name="melvinalves/teste:$branchName"
                        
                        docker build -t $image_name -f Dockerfile .
                        docker push $image_name
                        '''
                }
            }
        }
    }
}
