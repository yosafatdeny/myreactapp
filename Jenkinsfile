pipeline{
  agent any

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


  }
}