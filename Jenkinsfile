node {
    stages{
        stage('checkout'){
            step{
                checkout scm
            }
        }
        stage ('build'){
            step{
                sh npm install
            }
        }
        stage('test'){
            step{
                sh '''npm run ci-test || :
                npm run ci-lint || :'''
            }
        }
        stage ('checkstyle analysis report'){
            step{
                checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
            }
        }
        stage ('SonarQube Analysis'){
            step{
                def scannerHome = tool 'sonarScanner'
                withSonarQubeEnv('sonarQube'){
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=${SONAR_HOST_URL}  -Dsonar.login=${SONAR_AUTH_TOKEN}  -Dsonar.projectName=new-job -Dsonar.projectVersion=1.0 -Dsonar.projectKey=new-job -Dsonar.sources=index.js"
                }
            }
        }
    }
 
  }
  

    
            

