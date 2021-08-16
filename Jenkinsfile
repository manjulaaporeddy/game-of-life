pipeline {
    agent {label 'ANSIBLE'}
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
            }
        }
        stage('ansible') {
            agent{label 'ANSIBLE'}
            steps {
               sh 'cd deployment && ansible-playbook -i hosts deploy.yaml'
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
