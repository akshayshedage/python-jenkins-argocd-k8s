pipeline {
  agent any

  environment {
    IMAGE_TAG = "${BUILD_NUMBER}"
  }

  stages {
    stage('Checkout'){
      steps{
          git credentialsId: '',
          url: '',
          branch: 'main'
      }
    }

    stage('Build Docker'){
      steps{
        script{
          sh '''
          echo 'Build Docker Image'
          docker build -t abhishekf5/cicd-e2e:${BUILD_NUMBER} .
          '''
        }
      }
    }

    stage('Push the artifacts'){
      steps{
        script{
          sh '''
          echo 'Push to Repo'
          docker push abhishekf5/cicd-e2e:${BUILD_NUMBER}
          '''
        }
      }
    }

    stage('Checkout KBS manifest SCM'){
      steps{
        git credentialsId: '',
        url: '',
        branch: 'main'
      }
    }
    
  }
}
