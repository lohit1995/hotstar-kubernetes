pipeline{
    agent any
    tools{
        jdk 'jdk21'
        nodejs 'node'
    }
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    stages {
        stage('clean workspace'){
            steps{
                cleanWs()
            }
        }
        stage('Checkout from Git'){
            steps{
                git branch: 'main', ', url: 
            }
        }
       
                
       
        stage('Install Dependencies') {
            steps {
                sh "npm install"
            }
        }

           
        stage("Docker Build & Push"){
            steps{
                script{
                   withDockerRegistry(credentialsId: 'docker', toolName: 'docker'){   
                       sh "docker build -t hotstar ."
                       sh "docker tag hotstar lohitpunit/hotstar:latest "
                       sh "docker push lohitpunit/hotstar:latest "
                    }
                }
            }
        }
       
        stage('Deploy to container'){
            steps{
                sh 'docker run -d --name hotstar -p 3000:3000 lohitpunit/hotstar:latest'
            }
        }

    }
    

}
