pipeline {
    agent any
    triggers {
    GenericTrigger(
     genericVariables: [
      [key: 'ref', value: '$.ref']
     ],

     causeString: 'Triggered on $ref',

     token: '12345',
     tokenCredentialId: '',

     printContributedVariables: true,
     printPostContent: true,

     silentResponse: false,
   )
  }
    stages {
        stage('test') {
            steps {
                script {
                    input id: 'go', message: 'Proceed?', ok: 'Yes', submitter: 'admin'
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
    
        cleanup { 
            cleanWs()
        }
    }
}
