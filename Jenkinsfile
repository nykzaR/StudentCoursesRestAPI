pipeline {
    agent { label 'jackass' }
    triggers { pollSCM('* * * * *') }
    stages {
        stage('vcs') {
            steps {
                git url:'https://github.com/nykzaR/StudentCoursesRestAPI.git',
                    branch: 'develop'
            }
        }
        stage('build') {
            steps {
                sh 'docker image build -t aegonn/spc:latest .'
            }
        }
        stage('scan & push') {
            steps {
                sh 'echo docker scan aegonn/spc:latest'
                sh 'docker image push aegonn/spc:latest'
            }
        }
        stage('deploy to st') {
            steps {
                sh 'kubectl apply -f ./K8s/flask-aws.yml'
                sh 'kubectl apply -f ./K8s/mysql-aws.yml'
                sh 'sleep 9s'
                sh 'kubectl get svc'
            }
        }
    }
}