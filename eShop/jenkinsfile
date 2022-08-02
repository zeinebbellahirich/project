pipeline {

   agent any
  
  
   stages {
      stage(' Verify Branch ') {
           
         steps {
            echo 'Checking Branch..'
            echo "$GIT_BRANCH"
         }
       }
   
   
      
           
      stage(' Build Stage ') {
            steps {
            sh 'docker images -a'
            script { 
            sh 'docker build -t ms-frontend:1.0 frontend'
            sh 'docker build -t ms-products:1.0 products'
            sh 'docker build -t ms-shopping-cart:1.0 shopping-cart'
         
            
               }
            }
        }

      stage('Code Quality'){
      
      steps{
        sh 'echo Sonarqube Code Quality Check Done'
      }
      }

      stage('Test Stage ') {
            steps {
                echo 'Testing..'
               }
        }
      
      stage('Tag & Push docker images to ACR') {
      steps{
            echo 'loggin to Azure Container registry...'
            sh 'docker login --username edhriacr2022 --password uUqzNWODMutvpcWpFcK2/zvEqT5AMsM4 edhriacr2022.azurecr.io'
         
            sh '''  
            echo 'Pushing frontend docker image to azure container registry..'
            docker tag ms-frontend:1.0 edhriacr2022.azurecr.io/ms-frontend:1.0
            docker push edhriacr2022.azurecr.io/ms-frontend:1.0
            
            
            echo 'Pushing product docker image to azure container registry..'
            docker tag ms-products:1.0 edhriacr2022.azurecr.io/ms-products:1.0
            docker push edhriacr2022.azurecr.io/ms-products:1.0


         
            echo 'Pushing shopping-cart docker image to azure container registry..'
            docker tag ms-shopping-cart:1.0 edhriacr2022.azurecr.io/ms-shopping-cart:1.0
            docker push edhriacr2022.azurecr.io/ms-shopping-cart:1.0          

            '''
      }
    }

         
      
      stage('Deploy Stage') {
            steps {
                echo 'Deploying App to Kubernetes using ARGOCD..'
                   script {
                       echo ' ******************************** '
                         }
                  }
        }
}
}
