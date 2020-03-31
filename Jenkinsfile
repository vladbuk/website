pipeline {
   agent { node { label 'master' } }
   stages {
      stage('Git clone master branch') {
         steps {
            git 'https://github.com/vladbuk/website.git'
         }
      }
      stage('Hello Master') {
         steps {
            echo 'Hello World'
         }
      }
      stage('Run master docker container nginx') {
         steps {
            sh label: '', script: '''
                        pwd
                        docker start website-nginx || docker run --name website-nginx -d -p 80:80 -v "$(pwd)":/usr/share/nginx/html nginx
                        docker ps
                        ls -la
                        '''
         }
      }
   }
}
