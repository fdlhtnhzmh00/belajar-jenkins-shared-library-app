pipeline {
    agent {
        node {
            label "linux-agent" 
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Build process by Fadilah Tun Hazimah'
            }
        }
        stage('Test') {
            steps {
                echo 'Test process by Fadilah Tun Hazimah'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy process by Fadilah Tun Hazimah'
            }
        }
    }
    post {
        always {
            echo 'Fadilah: I will always say Hello again!' 
        }
        success {
            echo 'Yay, success!'
        }
        failure {
            echo 'Oh no, failure!'
        }
        cleanup {
            echo 'Don\'t care success or failure, just cleaning up!' 
        }
    }
}