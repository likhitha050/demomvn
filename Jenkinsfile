pipeline{
  agent any
  environment{
    DOCKER_CRED = credentials("dockerID")
    IMAGE_NAME = "cslikhitha/demomvn"
  }
  stages{
    stage('checkout'){
      steps{
        git(
          url:"https://github.com/likhitha050/demomvn.git",branch:"main"
        )
      }
    }
    stage("BUILD MAVEN"){
      steps{
        sh "mvn clean package -Dskiptests"
      }
    }
    stage('Build docker image'){
      steps{
        script{
         dockerImage = docker.build("${IMAGE_NAME}:latest") 
        }
      }
    }
    stage('Push Docker image'){
      steps{
        script{
          docker.withRegistry('https://index.docker.io/v1/','dockerID'){
            dockerImage.push()
          }
        }
      }
    }
  }
  post {
    success{
      echo "success... " 
    }
    failure{
      echo "failure..."
    }
    always{
      echo "cleaning..."
      deleteDir()
    }
  }
}
