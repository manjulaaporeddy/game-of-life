node('UBUNTU') {
    stage('scm') {
       git 'https://github.com/manjulaaporeddy/game-of-life.git'
    }
    stage('build'){
        sh 'mvn package'
    }
    stage('postbuild') {
       archive '**/*.war'
       junit '**/TEST-*.xml'
    }
}