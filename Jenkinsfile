pipeline{
  agent any
  environment {
    PATH = "${PATH}:${getTerraformPath()}"
	}
  stages{
    stage ('Package'){
      steps { 
        sh 'pushd shopfront/; mvn -Dmaven.test.failure.ignore=true clean install; popd' 
            }
        }
    }
	/*
	stage('TF-Destroy'){
	  steps{
	    sh "terraform destroy -auto-approve"
		}
	}
  */
 
  post {
	  always {
	    slackSend baseUrl: 'https://hooks.slack.com/services/',
        channel: '#devops-cicd', color: 'good',
        message: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
        teamDomain: 'govanin.slack.com',
        tokenCredentialId: 'slack-token'
	    }
	}
}

def getTerraformPath(){
  def tfHome = tool name: 'terraform12', type: 'terraform'
  return tfHome
  }