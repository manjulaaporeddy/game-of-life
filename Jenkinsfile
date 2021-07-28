pipeline {
    agent {label 'UBUNTU'}
    triggers {
        pollSCM('H * * * *')
    }
    parameters{
        choice(name: 'GOAL', choices: ['package', 'compile', 'clean package'], description: 'build the project') 
        string(name: 'BRANCH', defaultValue: 'master', description: 'branch to build')
            }
    stages {
        stage('SCM'){
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/manjulaaporeddy/game-of-life.git'
            }
        }
        stage('build'){
            steps {
                sh mvn "${params.GOAL}"
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
