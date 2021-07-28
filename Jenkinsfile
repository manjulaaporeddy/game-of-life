pipeline {
    agent {label 'UBUNTU'}
    triggers {
        pollSCM('H * * * *')
    }
    parameters{
        string(name: 'BRANCH', defaultValue: 'master', description: 'branch to build')
        choice(name: 'GOAL', choices: ['package', 'compile', 'clean package'], description: 'maven goals')
    }
    environment {
        DEVOPS = 'JENKINS'
    }   
    stages {
        stage('SCM'){
            environment {
                USER = 'MANJULA'
            }
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/manjulaaporeddy/game-of-life.git'
                echo env.DEVOPS
            }
        }
        stage('build'){
            steps {
                echo env.USER
                sh "mvn ${params.GOAL}"
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
