def server = Artifactory.server 'artifactory'
def JobDescription = "Sample Java pipeline Job"
def rtMaven = Artifactory.newMavenBuild()
def buildInfo = Artifactory.newBuildInfo()
  			buildInfo.env.capture = true
rtMaven.tool = 'maven3' //Maven tool name specified in Jenkins configuration
		 //If artifactory is not defined in Jenkins, then create on:
		// def server = Artifactory.newServer url: 'Artifactory url', username: 'username', password: 'password'
pipeline {
  agent any
  stages {
    stage('Checkout SCM') {
      steps {
        git(url: 'https://github.com/devops81/1282019.git', branch: 'master')
      }
    }

    stage('Tool Install') {
      steps {
        tool(name: 'java8', type: 'jdk')
        tool(name: 'maven3', type: 'maven')
      }
    }

    stage('Execute Maven') {
      steps {
        sh 'echo this will keep '
        script {
          script {
            rtMaven.run pom: '/var/lib/jenkins/workspace/DatabaseDevOps_master/examples/feed-combiner-java8-webapp/pom.xml', goals: 'clean install', buildInfo: buildInfo
          }
        }

      }
    }

    stage('Publish JUNIT') {
      steps {
        junit(testResults: 'examples/feed-combiner-java8-webapp/target/surefire-reports/*.xml', allowEmptyResults: true)
      }
    }

    stage('run-parallel-branches') {
      parallel {
        stage('A') {
          steps {
            sh 'echo "i am on step a"'
          }
        }

        stage('B') {
          steps {
            sh 'echo "i AM ON Step b"'
          }
        }

      }
    }

    stage('Post Actions') {
      steps {
        sh 'echo "i AM IN POST step"'
      }
    }

  }
}
