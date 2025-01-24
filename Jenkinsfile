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

    stage('Update K8S manifest & push to Repo'){
      steps{
        script{
          withCredentials([usernamePassword(credentailsId: '', passwordVariable: '')])
          sh '''
          cat deploy.yaml
          sed -i '' "s/32/${BUILD_NUMBER}/g" deploy.yaml
          cat deploy.yaml
          git add deploy.yaml
          git commit -m 'Updated the deploy yal | Jenkins Pipeline'
          git remote -v
          git push https://gith
          '''
        }
      }
    }
  }
}
