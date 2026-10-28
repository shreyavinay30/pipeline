pipeline{
   agent any
           
      environment{
        DOCKER_IMAGE="shreyavinay30/shreya"
        }
         
    stages{
       stage('Clone Repository'){
            steps{
                git branch: 'main',
                    url: 'https://github.com/shreyavinay30/pipeline.git'
}
}
    stage('Build Docker Image'){
       steps{
         "C:\Users\SHREYA\AppData\Local\Programs\DockerDesktop\resources\bin\docker.exe" build -t %DOCKER_IMAGE%:latest .
     }
  }
      stage('Login to DockerHub'){
            steps{
                withCredentials([strings(
                   credentialID: 'dockerhub-PAT',
                   variable: 'DOCKER-PAT'
          )])  { bat '''
                 @echo off
                 echo %DOCKER_IMAGE%|docker login -u shreyavinay30 --password-stdin
                 if errorlevel 1 exit /b 1
                '''
}
}
}
           stage('Push docker image'){
                 steps{
                     bat 'docker push %DOCKER_IMAGE%:latest'
            }
          }
    }
            post{
                 success{
                    echo 'docker image build and pushed successfully'
           }
             failure{
                 echo 'failed. check console output'
           }
        
        }
}
