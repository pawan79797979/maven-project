pipeline {
    agent any
     tools {
        maven 'localMaven'
    }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
                sh " sudo docker build . -t dockerhopper/app1:latest"
            }
            post {
                success {
                    withDockerRegistry([ credentialsId: "dockerhub", url: "" ]) {
                    sh 'docker push dockerhopper/app1:latest'
                    sudo sh 'ansible-playbook /etc/ansible/playbooks/credapp1.yml'
                }
            }
        }
    }
}
}
