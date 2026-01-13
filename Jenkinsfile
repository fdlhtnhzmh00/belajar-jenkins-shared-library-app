pipeline {
    agent none

    environment {
        AUTHOR = "Fadilah Tun Hazimah"
    }

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
        stage("OS Setup") {
            matrix {
                axes {
                    axis {
                        name "OS"
                        values "linux", "windows", "mac"
                    }
                    axis {
                        name "ARC"
                        values "32", "64"
                    }
                }

                excludes {
                    exclude {
                        axis {
                            name "OS"
                            values "linux"
                        }
                        axis {
                            name "ARC"
                            values "32"
                        }
                    }
                }

                stages {
                    stage("OS Setup") {
                        agent { node { label "linux-agent" } }
                        steps {
                            echo "Setup ${OS} ${ARC}" 
                        }
                    }
                }
            }
        } 

        stage("Preparation") {
            parallel {
                stage("Prepare Java") {
                    agent { node { label "linux-agent" } }
                    steps {
                        echo "Prepare Java by Fadilah Tun Hazimah"
                        sh "java -version"
                        sleep 5
                    }
                }
                stage("Prepare Maven") {
                    agent { node { label "linux-agent" } }
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
                APP = credentials('fadilah_rahasia')            
            }
            agent { node { label 'linux-agent' } }
            steps {
                echo "Hello ${params.NAME}"
                echo "Need to deploy : ${params.DEPLOY}"
                echo "Pipeline authorized by ${AUTHOR}"
            }
        }

        stage('Build') {
            agent { node { label "linux-agent" } }
            steps {
                script {
                    for (int i = 0; i < 5; i++) {
                        echo "Script Iterasi ke-${i}"
                    }
                }
                echo "Start Build by Fadilah Tun Hazimah"
                sh 'chmod +x mvnw'
                sh './mvnw clean compile test-compile'
            }
        }

        stage('Test') {
            agent { node { label "linux-agent" } }
            steps {
                script {
                    def data = [ "firstName": "Fadilah", "lastName" : "Tun Hazimah" ]
                    writeJSON(file: "data.json", json: data) 
                }
                echo "Running Test..."
                sh './mvnw test'
            }
        }

        stage('Deploy') {
            input {
                message "Fadilah, can we deploy this to production?"
                ok "Yes, of course"
                submitter "fdlhtnhzmh,zowy" 
            }
            agent { node { label "linux-agent" } }
            steps {
                echo "Deploying application..."
                sleep(2)
            }
        }

        stage('Release') {
            when {
                expression { return params.DEPLOY }
            }
            agent { node { label 'linux-agent' } }
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "fadilah_rahasia",
                    usernameVariable: "USER",
                    passwordVariable: "PASSWORD"
                )]) {
                    sh 'echo "Release it with -u $USER -p $PASSWORD" > release.txt'
                    sh 'cat release.txt'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline Finished. Cleaning up...'
        }
        success {
            echo 'Build SUCCESS!'
        }
        failure {
            echo 'Build FAILED!'
        }
    }
}