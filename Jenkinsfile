pipeline{
    agent any
        // docker{image 'python:3.10-slim-buster'
        // args '--user root -v /var/run/docker.sock:/var/run/docker.sock' }
    environment{
        IMAGE_TAG="$BUILD_NUMBER"
        DOCKER_CREDENTIALS=credentials("Aditya-dockerhub")
    }
    stages{
        stage('clean workspace'){
            steps{
                sh 'echo Cleaning the Workspace Before Building '
                // sh 'docker-compose down'
                // sh 'docker system prune -a -f '
            }
        }
        // stage('SCM'){
        //     steps{
        //         sh 'pwd '
        
        //         sh 'git clone https://github.com/Adityac115/Flask-Learning.git '
        //     }
        // }
        stage('Build'){
            steps{
                sh' echo Building Docker image'
                sh 'docker build -t aditya115/todo-app:${IMAGE_TAG} .'
        }
        }
        stage('Testing'){
            steps{
                sh 'echo Testing...'
            }
        }
//         stage('Sonarqube') {
//     environment {
//         scannerHome = tool 'SonarQubeScanner'
//     }
//     steps {
//         withSonarQubeEnv('sonarqube') {
//             sh "${scannerHome}/bin/sonar-scanner"
//         }
//         timeout(time: 10, unit: 'MINUTES') {
//             waitForQualityGate abortPipeline: true
//         }
//     }
// }
        stage('Push to Dockerhub'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'Aditya-dockerhub') {

                    sh 'echo Login to dockerhub.... '
                    sh ' docker push aditya115/todo-app:${IMAGE_TAG} '
                    }
            }
        }
            
        }
        stage('Deploy'){
            steps{
                sh 'echo Deploying...'
                sh'pwd'
                sh 'docker-compose up -d --build --remove-orphans '
                // '--scale flask-app=5 '
            }
        }   
    
}
}

