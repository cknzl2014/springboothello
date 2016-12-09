#!groovy

def project = env.JOB_NAME.split('/')[env.JOB_NAME.split('/').length -2]
def jobshortname = env.JOB_NAME.substring(env.JOB_NAME.lastIndexOf('/') + 1)
def shortname = jobshortname.substring(jobshortname.indexOf('-') + 1)
def dockerImageName = shortname.substring(shortname.indexOf('-') + 1)
def dockerRegistry = 'http://nexus.vcap.me:5000'
def dockerRepository = 'yourrepository'
def dockerCredentialsId = 'docker'

node {
    stage('Checkout') {
        checkout scm
    }

    def dockerImageTag = sh(returnStdout: true, script: 'git describe --all').trim().replaceAll(/(.*\/)?(.+)/,'$2')


    stage('Env') {
        echo "*** Show env variables: ***" + \
	"\n JOB_NAME: " + env.JOB_NAME + \
	"\n Project: " + project + \
	"\n Jobshortname: " + jobshortname + \
	"\n Shortname: " + shortname + \
	"\n dockerRegistry: " + dockerRegistry + \
	"\n dockerRepository: " + dockerRepository + \
	"\n dockerCredentialsId: " + dockerCredentialsId + \
	"\n dockerImageName: " + dockerImageName + \
	"\n dockerImageTag: " + dockerImageTag
    }
    stage('Docker Build') {
        docker.withRegistry(dockerRegistry, dockerCredentialsId) {
	    def image = docker.build dockerRepository + "/" + dockerImageName, "--build-arg TAG=${dockerImageTag} ."
	    //image.push(dockerImageTag)
	    echo "*** Docker image successfully pushed to registry. ***"
	}
    }
    //stage('Maven') {
    //    docker.image('maven:3.3.3-jdk-8').inside('-p 5000:5000') {
    //    writeFile file: 'settings.xml', text: "<settings><localRepository>${pwd()}/.m2repo</localRepository><mirrors><mirror><id>nexus</id><url>http://nexus.vcap.me:5000</url><mirrorOf>*</mirrorOf></mirror></mirrors></settings>"
    //        sh 'mvn -B -s settings.xml clean install'
    //    }
    //}
}
