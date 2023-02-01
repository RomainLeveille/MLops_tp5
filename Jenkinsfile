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
  }
}
