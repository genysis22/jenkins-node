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
            
}
