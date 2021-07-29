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
            steps {
                git branch: "${params.BRANCH}", url: 'https://github.com/manjulaaporeddy/game-of-life.git'
            }    
        }
        stage('build'){
            steps {
                sh "mvn ${params.GOAL}"
                stash includes: '**/game-of-life.war', name: 'golwar'

            }
        }
        stage('devserver') {
            agent{label REDHAT}
            steps {
                unstash name: 'golwar'
            }
        }                
                  
    post {
      success {
         archive '**/*.war'
         junit '**/TEST-*.xml'
        }
        
    }
}
