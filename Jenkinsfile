pipeline {
    agent any
    stages {
        stage('test') {
            steps {
                script {
                    input message: 'Proceed?', ok: 'Yess', submitter: 'admin'
                }
                echo "helloworld"
            }
            post {
                aborted{
                    echo "Test stage has been aborted."
                }
            }            
        }
    }
    post {
        aborted {
            echo "Pipeline has been aborted."
        }
    }
}
