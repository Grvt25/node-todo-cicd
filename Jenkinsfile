pipeline{
    agent {label 'dev'}
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/Grvt25/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('Build and test'){
            steps{
                sh 'docker build . -t garvit25/node-todo-app-cicd:latest'
            }
        }
        stage('Logging and push image'){
            steps{
                echo 'loging in to docker hub and pushing image..'
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dokerHubPassword',usernameVariable:'dockerHubUser')]){
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dokerHubPassword}"
                    sh "docker push garvit25/node-todo-app-cicd:latest"
                }
            }
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
