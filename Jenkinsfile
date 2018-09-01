  
// properties([parameters([choice(choices: 'sbt', description: 'Select Project to build', name: 'PROJECT')])])

  properties([pipelineTriggers([upstream('baskar-test')])])

node{

    stage('Deploy Offerings to Test Env'){
        // env.DEPLOY_REGION=test
        def offerings_build = findRecentSuccessBuild('build.offerings')
        def enspire_oms_build = findRecentSuccessBuild('build.enspire-oms')
        build job: 'deploy.vpc.test', parameters: [string(name: 'PROJECT', value: 'sbt'), 
            string(name: 'RELEASE', value: '170'), booleanParam(name: 'ROLLING', value: false), 
            booleanParam(name: 'EXCEPTIONS', value: true), 
            booleanParam(name: 'KILL', value: false), 
            string(name: 'TIMEOUT', value: '30'), 
            string(name: 'OFFERINGS', value: offerings_build), 
            string(name: 'ENSPIRE_OMS', value: enspire_oms_build)]
      
    }
    stage('Run Selenium Test Cases'){
      build 'selenium.test'
    }
 
    
}

def findRecentSuccessBuild(def job_id){
    def job, successBuild
    job = jenkins.model.Jenkins.instance.getItem(job_id)
    job.builds.each {
      if (it.getResult().toString().equals("SUCCESS") ) {
        successBuild = it.displayName
        return true
      }
    }
    successBuild
    
}
