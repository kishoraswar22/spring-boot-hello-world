pipeline {
    agent any
    tools {
        jdk 'jdk17'
        maven 'maven' 
    }
    
    environment{
        SCANNER_HOME= tool 'sonar-scanner'
        
    }
    

    stages {
        stage('Code Checkout') {
            steps {
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/kishoraswar22/spring-boot-hello-world.git'
            }
        }
    stage(' Build') {
            steps {
                sh 'mvn  package'
        }
    }

    stage(' Test') {
            steps {
                sh 'mvn  test'
        }
    }
    stage(' Sonar Analysis') {
            steps {
                 withSonarQubeEnv('sonar') {
                  sh '''
                  $SCANNER_HOME/bin/sonar-scanner   -Dsonar.projectName=SpringApp -Dsonar.projectKey=SpringApp  -Dsonar.java.binaries=.  -Dsonar.sources=.
                  '''
                       
                 }
            }
       }

    stage(' Dev Deployment') {
            steps {
                  echo "dev deployment"
        }
    }
    stage('UAT Deployment') {
            steps {
                echo 'uat deployment'
        }
    }
    stage(' PROD Deployment') {
            steps {
                echo 'Prod deployment'
        }
    }
    }
}
