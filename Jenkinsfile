pipeline{
    agent any
    tools {
           maven 'Maven3'
         }
    stages{
        stage('checkout the code from github'){
            steps{
                 git 'https://github.com/karthikpyati777/Banking-java-project.git'
                 echo 'github url checkout'
            }
        }
        stage('code compile with karthik'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('code testing with karthik'){
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
        stage('Build Docker image'){
          steps{
               sh 'docker build -t karthik854/financeme:latest .'

           }
         }
        stage('Docker Login Credenials'){
          steps{
              withCredentials([usernamePassword(credentialsId: 'dockeruserid', passwordVariable: 'dockerhubuserpw', usernameVariable: 'dockerhubusername')]) {
               sh "docker login -u ${dockerhubusername} -p ${dockerhubuserpw}"
              }
           }
         }
        stage('port expose'){
            steps{
                   sh 'docker run -d -p 8096:8081 karthik854/financeme:latest'
            }
        } 

      stage('Deploy Application using Ansible') {
         steps {
		ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'Ansible2', inventory: '/etc/ansible/hosts', playbook: 'ansible-playbook.yml', vaultTmpPath: ''
            }
      }
          
      }
}	
