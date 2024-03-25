pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven-3.9.6"
    }

    stages {
        stage('git-clone') {
            steps {
                git branch: 'kubernetes', url: 'https://github.com/priyabratswain009/springboot-practice.git'
     

        }
   }
 
        stage('service-registryr') {
            when {
                changeset '**/service-registry/**'
            }
            steps {
                 dir('service-registry') {
                     sh 'mvn clean package'
                     sh 'docker build -t registry .'
                     sh 'docker login -u priyabrat.swn009@gmail.com -p 7008330675'
                     sh 'docker tag registry priyabratswainn009/spring:registry-1.0'
                     sh "docker push priyabratswainn009/spring:registry-1.0"
        
                }
            }
               
        } 
        
        stage('user-service') {
            when{
                 changeset '**/user-service/**'
            }
            steps {
                 dir('user-service') {
                     sh 'mvn clean package'
                     sh 'docker build -t userservice .'
                     //sh 'docker login -u priyabrat.swn009@gmail.com -p 7008330675'
                     sh 'docker tag userservice priyabratswainn009/spring:userservice'
                     sh "docker push priyabratswainn009/spring:userservice"
        
                }
            }
               
        }    
        stage('department-service') {
            when{
                changeset '**/department-service/**'
            }
            steps {
                 dir('department-service') {
                     sh 'mvn clean package'
                     sh 'docker build -t department .'
                     //sh 'docker login -u priyabrat.swn009@gmail.com -p 7008330675'
                     sh 'docker tag department priyabratswainn009/spring:department'
                     sh "docker push priyabratswainn009/spring:department"
        
                }
            }
               
        }  
        stage('cloud-gateway') {
            when{
              changeset '**/cloud-gateway/**'
            }
            steps {
                 dir('cloud-gateway') {
                     //sh 'mvn clean package'
                     //sh 'docker build -t gateway .'
                     //sh 'docker login -u priyabrat.swn009@gmail.com -p 7008330675'
                     sh 'docker tag gateway priyabratswainn009/spring:gateway'
                     sh "docker push priyabratswainn009/spring:gateway"
        
                }
            }
               
        } 
        
        stage('cloud-config-server') {
            when{
                changeset '**/cloud-config-server/**'
            }
            steps {
                 dir('cloud-config-server') {
                     sh 'mvn clean package'
                     sh 'docker build -t configserver .'
                     //sh 'docker login -u priyabrat.swn009@gmail.com -p 7008330675'
                     sh 'docker tag configserver priyabratswainn009/spring:configserver'
                     sh "docker push priyabratswainn009/spring:configserver"
        
                }
            }
               
        } 
        
        stage('eks'){
            steps{
                sshagent(['eks']) {
                   sh "scp -o StrictHostKeyChecking=no -r ./kubernetes-manifest/*  ubuntu@54.84.5.226:/home/ubuntu/efk  "
                   sh "ssh -o StrictHostKeyChecking=no   ubuntu@54.84.5.226 'kubectl get all'  "
                    
                }
            }
            
        }
} 
}
