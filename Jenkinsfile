pipeline {
    agent any
    stages {

        stage('Clone Repo') {
          steps {
            sh 'rm -rf dockertest1'
            sh 'git clone https://github.com/saigopichand/dockertest.git'
            }
        }

        stage('Build Docker Image') {
          steps {
            sh 'cd /var/lib/jenkins/workspace/pipeline2/dockertest1'
            sh 'cp  /var/lib/jenkins/workspace/pipeline2/dockertest1/* /var/lib/jenkins/workspace/pipeline2'
            sh 'docker build -t gopichand1907/pipelinetest:v1 .'
            }
        }

        stage('Push Image to Docker Hub') {
          steps {
           sh    'docker push gopichand1907/pipelinetest:v1'
           }
        }https://github.com/nareshmanojari1/dockertest1.git
        stage('Deploy to Docker Host') {
          steps {
            sh    'docker -H tcp://10.1.1.200:2375 stop webapp1'
            sh    'docker -H tcp://10.1.1.200:2375 run --rm -dit --name webapp1 --hostname webapp1 -p 9000:80 gopichand1907/pipelinetest:v1'
            }
        }

        stage('Check WebApp Rechability') {
          steps {
          sh 'sleep 10s'
          sh 'curl ec2-3-93-188-153.compute-1.amazonaws.com:9000'
          }
        }

    }
}
