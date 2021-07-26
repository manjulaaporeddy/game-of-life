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
       mail bcc: '', body: 'em chettannav ra', cc: '', from: '', replyTo: '', subject: 'build fail', to: 'vivekreddysandhi@gmail.com'
    }
}