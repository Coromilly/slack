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
                    echo "test stage has been aborted."
                }
            }            
        }
    }
    post {
        aborted {
            echo "pipeline has been aborted."
        }
    }
}
