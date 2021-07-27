pipeline {
    agent {label 'UBUNTU'}
    triggers {
        cron('H * * * *')
        pollSCM('* * * * *')
    }
    parameters{
        string(name: 'BRANCH', defaultvalue: 'master', description: 'branch to build')
    }
    stages {
        stage('SCM'){
            steps {
                git branch: 'master', url: 'https://github.com/manjulaaporeddy/game-of-life.git'
            }
        }
        stage('build'){
            steps {
                sh 'mvn package'
                input 'continue to next stage?'
                }   
            } 
        }    
    post {
      success {
         archive '**/*.war'
         junit '**/TEST-*.xml'
    }
        failure {
          echo 'build fail'
        }
    }
}
