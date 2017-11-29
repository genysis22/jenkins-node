#!groovy
import groovy.json.JsonSlurper
pipeline {
    agent any
    stages{
        stage('checkout'){
            steps{
                checkout scm
            }
        }
        stage ('build'){
            steps{
                sh npm install
            }
        }
        stage('test'){
            steps{
                sh '''npm run ci-test || :
                npm run ci-lint || :'''
            }
        }
        stage ('checkstyle analysis report'){
            steps{
                checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
            }
        }
        stage ('SonarQube Analysis'){
            def scannerHome = tool 'sonarScanner'
            steps{
                withSonarQubeEnv('sonarQube'){
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=${SONAR_HOST_URL}  -Dsonar.login=${SONAR_AUTH_TOKEN}  -Dsonar.projectName=new-job -Dsonar.projectVersion=1.0 -Dsonar.projectKey=new-job -Dsonar.sources=index.js"
                }
            }
        }
    }
}
 
  
  

    
            

