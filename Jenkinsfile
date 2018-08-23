
node {
   def builds = [""]
   def job_id = "deploy.vpc.test"
   def job = jenkins.model.Jenkins.instance.getItem(job_id)

stage(deploy) {
      build job: "job_id",  
      properties([hudson.plugins.buildblocker.BuildBlockerProperty plugin="build-blocker-plugin@1.7.3"]
            [useBuildBlocker=false]
            [blockLevel=GLOBAL]
            [scanQueueFor=DISABLED]), parameters([choice(choices: ['oms', 'b2bmb', 'sbt'], description: '', name: 'PROJECT'), choice(choices: ['144', '145', '152', '153', '154'], description: '', name: 'RELEASE'), booleanParam(defaultValue: false, description: '', name: 'ROLLING'), booleanParam(defaultValue: false, description: '', name: 'EXCEPTIONS'), booleanParam(defaultValue: false, description: '', name: 'KILL'), choice(choices: ['30', '60', '120', '300', '600'], description: '', name: 'TIMEOUT'), [$class: 'ExtensibleChoiceParameterDefinition', choiceListProvider: [$class: 'SystemGroovyChoiceListProvider', groovyScript: [classpath: [], sandbox: true, 
script: '''def builds = [""]
def job_id = "build.offerings"

def job = jenkins.model.Jenkins.instance.getItem(job_id)
job.builds.each {
  if (it.getResult().toString().equals("SUCCESS") && builds.size() <= 51) {
    builds.add(it.displayName)
  }
}

builds.unique();
'''], usePredefinedVariables: false], description: '', editable: false, name: 'OFFERINGS'], [$class: 'ExtensibleChoiceParameterDefinition', choiceListProvider: [$class: 'SystemGroovyChoiceListProvider', groovyScript: [classpath: [], sandbox: true, script: '''def builds = [""]
def job_id = "build.enspire-oms"

def job = jenkins.model.Jenkins.instance.getItem(job_id)
job.builds.each {
  if (it.getResult().toString().equals("SUCCESS") && builds.size() <= 51) {
    builds.add(it.displayName)
  }
}

builds.unique();'''], usePredefinedVariables: false], description: '', editable: false, name: 'ENSPIRE_OMS']]) }
}
