pipeline{
    agent any
    stages{
        stage('checkout the code from github'){
            steps{
                 git 'https://github.com/karthikpyati777/Banking-java-project.git'
                 echo 'github url checkout'
            }
        }
        stage('codecompile with karthik'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('codetesting with karthik'){
            steps{
                sh 'mvn test'
            }
        }
        stage('qa with karthik'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('package with karthik'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('run dockerfile'){
          steps{
               sh 'docker build -t myimg .'
           }
         }
        stage('port expose'){
            steps{
                sh 'docker stop myimg'
                sh 'docker rm myimg'
                sh 'docker run -dt -p 8091:8091 --name c000 myimg'
            }
        }   
    }
}
