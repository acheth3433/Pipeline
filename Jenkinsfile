@Library('piper-lib-os') _
node() {
    stage('prepare') {
        checkout scm 
        setupCommonPipelineEnvironment script: this
    }
    stage('build')
    {
        mtaBuild script: this
    }
    stage('Jenkins')
    {
       karmaExecuteTests script: this,
	       dockerImage: node:lts-alpine3.15,
        installCommand: "npm config set @sap:registry https://npm.sap.com && npm install --quiet", 
	  runCommand: 'npm test'
    }
    stage('deploy') 
    {
        cloudFoundryDeploy script: this
    }
    
}
