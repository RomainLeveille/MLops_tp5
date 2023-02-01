pipeline {
  agent any
 
  stages{
    stage('hello word ! :)'){
      steps{
        echo 'Hello Word :)'
      }
    }
    stage('create staging'){
      steps{
        echo 'create a staging branch'
        sshagent(credentials: ['668ba457-0dba-4cf9-b05f-cc864cfd46eb']){
          bat 'git checkout -B staging'//create staging if not exists, and overwrite it if it exists
          bat 'git push origin staging'
          bat 'git branch'
        }
        echo 'branch created'
        
      }
    }
    stage('Test Python Program') {
      steps {
        echo 'installing python'
        bat 'pip install -r requirements.txt'
        bat 'python -m test_main'
      }
    }
    stage('Docker Image'){
      steps{
        echo 'building docker image'
        bat 'docker build -t monimage .'
                
        echo'pushing to docker hub'
        bat 'docker login -u romain1806 -p dckr_pat_kSx8KoxvfaaiegnNyjQxcZ5FxBc'
        bat 'docker tag monimage romain1806/pipelinetp5:latest'
        bat 'docker push romain1806/pipelinetp5:latest'
        
        echo 'running the image'
        bat 'docker run -d monimage'
      }
    }
   /* stage('merging'){
      steps{
        sshagent(credentials: ['8b03b3ed-9573-42b2-b121-b94740feccde']){
          #
          echo 'merging to main'
          bat 'git push origin main'
          bat 'git checkout main'
          
          bat'git config user.name "MatthieuHanania"'
          bat'git config user.email "matthieu.hanania@efrei.net"'
          bat'git add *'       
          
          echo "pushing"
          //bat 'git merge staging'
          bat 'git reset --hard origin/staging' //staging becomes the main

          bat 'git push -f origin main'
          //bat 'git push origin -d staging'
          #
          
          bat'git fetch origin'
          
          //bat'git checkout staging'
          //bat'git merge origin/staging'
          
          bat'git checkout main'
          bat'git merge origin/main'
          
          bat'git merge -X theirs staging'
          bat'git push origin main '
          
        }
      }
    }
*/
  }
}
