pipeline{
  agent any

  environment {
    DOCKER_TAG = getDockerTag()
  }
  stages{
    
    stage ('install dependencies'){
      steps{
        echo "start install dependencies"  
        sh "npm install"  
      }
    }
    stage ('test project'){
      steps{
        echo "run test project"
      }
    }
    stage ('Build'){
      steps{
      sh 'npm run build'
      }
    }
    stage ('build docker image'){
      steps{
        script{
          app = docker.build("yosafatdeny/myreactapp")
        }
      }
    }
    stage ('test image'){
      steps{
        sh'docker run -d --rm --name testcontainer -p 8081:80 yosafatdeny/myreactapp'
      }
    }
    stage ('cleanup docker'){
      steps{
        sh 'docker stop testcontainer'
      }
    }
    stage ('push image'){
      steps{
        script{
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-yosafatdeny'){
            app.push("${DOCKER_TAG}")
          }
        }
      }
    }
  }
}

def getDockerTag(){
  def tag = sh script: "git rev-parse HEAD", returnStdout: true
  return tag
}