pipeline {
    agent none

    environment {
        AUTHOR = "Fadilah Tun Hazimah"
    }

    //triggers {
    //    cron ("*/5 * * * *")
    // }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to Deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ["Instagram", "Facebook", "Twitter"], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }
    
    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {
        stage("Preparation") {
            parallel {
                stage("Prepare Java") {
                    agent { 
                        node { 
                            label "linux-agent" } }
                    steps {
                        echo "Prepare Java by Fadilah Tun Hazimah"
                        sh "java -version"
                        sleep 5
                    }
                }
                stage("Prepare Maven") {
                    agent { 
                        node { 
                            label "linux-agent" } }
                    steps {
                        echo "Prepare Maven by Fadilah Tun Hazimah"
                        sh "./mvnw --version"
                        sleep 5
                    }
                }
            }
        }


        stage('Prepare') {

            environment {
                APP = credentials('fadilah_rahasia')            }

            agent {
                node { label 'linux-agent' }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "Your description is ${params.DESCRIPTION}"
                echo "Your social media is ${params.SOCIAL_MEDIA}"
                echo "Need to deploy : ${params.DEPLOY} to deploy!"
                echo "Your secret is ${params.SECRET}"
                
                echo "Pipeline authorized by ${AUTHOR}"
            }
        }
        stage('Build') {
            agent {
        node {
            label "linux-agent" 
        }
    }
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
            agent {
        node {
            label "linux-agent" 
        }
    }
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
            input {
                message "Fadilah, can we deploy this to production?"
                ok "Yes, of course"
                submitter "fdlhtnhzmh,zowy" 
            }

            agent {
        node {
            label "linux-agent" 
        }
    }
            steps {
                echo "Hello Deploy 1 by Fadilah Tun Hazimah"
                sleep(5)
                echo "Hello Deploy 2 by Fadilah Tun Hazimah"
                echo "Hello Deploy 3 by Fadilah Tun Hazimah"
            }
        }
        stage('Release') {
            when {
                expression {
                    return params.DEPLOY
                }
            }
            
            agent { 
                node { 
                    label 'linux-agent' } }

            steps {
                echo "Release it by Fadilah Tun Hazimah"
                sh 'echo "Application Released to Production!"'
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