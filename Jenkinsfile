pipeline {
    agent any
    stages{
        stage('git cloned'){
            steps{
                git url:'https://github.com/shubhamgunjal198/php-project.git/', branch: "master"
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t shubhamgunjal199/myimage01:v1 .'
                    sh 'docker images'
                }
            }
        }
          stage('Docker login') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'dock-cred', 
            usernameVariable: 'USER', 
            passwordVariable: 'PASS'
        )]) {
            sh '''
                echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                docker push shubhamgunjal199/myimage01:v1
            '''
        }
    }
}
        
     stage('Deploy') {
            steps {
               script {
                   def dockerrm = 'sudo docker rm -f My-first-containe2211 || true'
                    def dockerCmd = 'sudo docker run -itd --name My-first-containe2211 -p 8083:80 shubhamgunjal199/myimage01:v1'
                    sshagent(['sshkeypair']) {
                        //chnage the private ip in below code
                        // sh "docker run -itd --name My-first-containe2111 -p 8083:80 shubhamgunjal199/2febimg:v1"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.27.250 ${dockerrm}"
                         sh "ssh -o StrictHostKeyChecking=no ubuntu@172.31.27.250 ${dockerCmd}"
                    }
                }
            }
        }
    }
}
