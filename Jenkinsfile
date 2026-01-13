pipeline {
    agent {
        node {
            label "linux-agent" 
        }
    }
    stages {
        stage('Build') {
            steps {
                script {
                    for (int i = 0; i < 10; i++) {
                        echo "Script Iterasi ke-${i} by fdlhtnhzmh"
                    }
                }

                echo "Start Build by Fadilah Tun Hazimah"
                sh 'chmod +x mvnw'
                sh './mvnw clean compile test-compile'
                echo "Finish Build by Fadilah Tun Hazimah"
            }
        }
        stage('Test') {
            steps {
                script {
                    def data = [
                        "firstName": "Fadilah",
                        "lastName" : "Tun Hazimah"
                    ]
                    writeJSON(file: "data.json", json: data) 
                }

                echo "Start Test by Fadilah Tun Hazimah"
                sh './mvnw test'
                echo "Finish Test by Fadilah Tun Hazimah"
            }
        }
        stage('Deploy') {
            steps {
                echo "Hello Deploy 1 by Fadilah Tun Hazimah"
                sleep(5)
                echo "Hello Deploy 2 by Fadilah Tun Hazimah"
                echo "Hello Deploy 3 by Fadilah Tun Hazimah"
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