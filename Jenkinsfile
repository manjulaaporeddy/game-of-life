pipeline {
    agent {label 'UBUNTU'}
    stages {
        stage('SCM'){
            steps {
                git branch: 'master', url: 'https://github.com/manjulaaporeddy/game-of-life.git'
            }
        }
        stage('build'){
            steps {
                sh 'mvn package'
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
