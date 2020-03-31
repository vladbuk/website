pipeline {
   agent { label 'linux' }
   stages {
      stage('Hello Slave') {
         steps {
            echo 'Hello Slave World'
         }
      }
      stage('Git clone dev branch') {
         steps {
            git branch: 'dev', url: 'https://github.com/vladbuk/website.git'
         }
      }
      stage('Run slave docker container nginx') {
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
