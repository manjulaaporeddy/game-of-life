pipeline {
    agent {label 'UBUNTU'}
    triggers {
        cron('H * * * *')
        pollSCM('H * * * *')
    }
    parameters{
        string(name: 'BRANCH', defaultValue: 'master', description: 'branch to build')
        choice(name: 'MAVEN_GOAL', choices: ['package', 'compile', 'clean'], description: 'this is to build the project')
    }
    stages {
        stage('SCM'){
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/manjulaaporeddy/game-of-life.git'
            }
        }
        stage('build'){
            steps {
                sh mvn "${params.MAVEN_GOAL}"
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
