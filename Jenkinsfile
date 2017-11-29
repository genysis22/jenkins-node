node {
    stage 'checkout'
    checkout scm        
        
     // git 'https://github.com/genysis22/jenkins-node.git'
    
    stage 'build, test'
    sh '''npm install
    npm run ci-test || :
    npm run ci-lint || :'''
    
    stage 'checkstyle analysis report'
    checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: ''
    
    stage 'SonarQube Analysis'
    def scannerHome = tool 'sonarScanner'
    withSonarQubeEnv('sonarQube') 
    sh "${scannerHome}/bin/sonar-scanner -Dsonar.host.url=${SONAR_HOST_URL}  -Dsonar.login=${SONAR_AUTH_TOKEN}  -Dsonar.projectName=new-job -Dsonar.projectVersion=1.0 -Dsonar.projectKey=new-job -Dsonar.sources=index.js"
 
  }
  

    
            

