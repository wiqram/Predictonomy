node {
  stage 'Checkout'
  //git 'https://github.com/wiqram/Predictonomy.git", credentialsId: '7b88f88d-a254-41d8-90fb-6b6cb399bfcf'
  git url: "https://github.com/wiqram/Predictonomy.git", credentialsId: '7b88f88d-a254-41d8-90fb-6b6cb399bfcf'
  sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
 
 
  stage 'Docker build'
  docker.build('predictonomy/repo')
 
  stage 'Docker push'
  docker.withRegistry('https://068478564052.dkr.ecr.eu-west-2.amazonaws.com', '068478564052') {
    docker.image('predictonomy/repo').push("${commit_id}")
  }
}