pipeline {
    agent any
    tools { git 'Default' }
    stages {
        stage('Create staging branch') {
            steps {
                bat 'git branch -d staging'
                bat 'git branch staging'
                bat 'git checkout staging'
            }
        }
        stage('Build and test') {
            steps {
                bat 'pip install -r requirements.txt'
                bat 'pytest'
                bat 'docker run hello-world'
                bat 'docker build -t myimage .'
                // When I launch the Docker run, the build never stop. So I don't launch it here
                //bat 'docker run myimage'
                bat 'docker login -u romain1806 -p dckr_pat_kSx8KoxvfaaiegnNyjQxcZ5FxBc'
                bat 'docker push romain1806/docker_jenkins_use'
            }
        }
        
        stage('Push') {
            steps {
                sshagent(credentials: ['668ba457-0dba-4cf9-b05f-cc864cfd46eb']){
                    bat "git push origin staging"
                }
            }
        }
        
        stage('Merge to main branch') {
            steps {
                sshagent(credentials: ['668ba457-0dba-4cf9-b05f-cc864cfd46eb']){
                    bat 'git checkout main'
                    bat 'git merge staging'
            
                }
            }
        }
        
        
    }
}


