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
                USERDEV = 'MANJULA'
            }
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/manjulaaporeddy/game-of-life.git'
                echo env.$GIT_URL
                echo env.$WORKSPACE
                echo env.DEVOPS
            }
        }
        stage('build'){
            steps {
                echo env.USERDEV
                sh 'set'
                sh "mvn ${params.GOAL}"
                echo env.$BUILD_URL
                }   
            } 
        }    
    post {
      success {
         archive '**/*.war'
         junit '**/TEST-*.xml'
        }
        
    }
}
