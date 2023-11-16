pipeline {
    agent { 
        node {
            label 'docker-agent-python'
            }
      }
    triggers {
        pollSCM '* * * * *' // this will check the code in version control every 1 min and triggers the build automatically
    }
    stages {
        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                pip install -r requirements.txt
                '''
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                python3 hello.py
                '''
            }
        }

        stage('Test Hello World') {
            steps {
                script {
                    // Read the content of the helloworld.py file
                    def fileContent = readFile 'helloworld.py'

                    // Check if "Hello World" is present in the file content
                    if (fileContent.contains('Hello World')) {
                        echo 'The string "Hello World" is present in helloworld.py'
                    } else {
                        error 'The string "Hello World" is not present in helloworld.py'
                    }
                }
            }
        }
        stage('Deliver') {
            steps {
                echo 'Deliver....'
                sh '''
                echo "doing delivery stuff.."
                '''
            }
        }
    }
}