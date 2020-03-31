pipeline {
   agent none
   stages {
      stage('Git clone master branch') {
         agent { node { label 'master' } }
         steps {
            git 'https://github.com/vladbuk/website.git'
         }
      }
      stage('Hello Master') {
         agent { node { label 'master' } }
         steps {
            echo 'Hello World'
         }
      }
      stage('Run master docker container nginx') {
         agent { node { label 'master' } }
         steps {
            sh label: '', script: '''
                        pwd
                        docker start website-nginx || docker run --name website-nginx -d -p 80:80 -v "$(pwd)":/usr/share/nginx/html nginx
                        docker ps
                        ls -la
                        '''
         }
      }
      stage('Hello Slave') {
         agent { label 'linux' }
         steps {
            echo 'Hello World'
         }
      }
      stage('Git clone dev branch') {
         agent { label 'linux' }
         steps {
            git branch: 'dev', url: 'https://github.com/vladbuk/website.git'
         }
      }
      stage('Run slave docker container nginx') {
         agent { label 'linux' }
         steps {
            sh label: '', script: '''
                        pwd
                        docker start website-nginx || docker run --name "$name" -d -p 80:80 -v "$(pwd)":/usr/share/nginx/html nginx
                        docker ps
                        ls -la
                        '''
         }
      }
   }
}
