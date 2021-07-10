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

     printContributedVariables: false,
     printPostContent: false,

     silentResponse: false,
   )
  }
    stages {
        stage('test') {
            steps {

                blocks = [
                    [
                        "type": "section",
                        "text": [
                            "type": "mrkdwn",
                            "text": "Hello, please accept job."
                        ]
                    ],
                    [
                        "type": "divider"
                    ],
                    [
                        "type": "actions",
                        "elements": [
                            [
                                "type": "button",
                                "text": [
                                    "type": "plain_text",
                                    "emoji": true,
                                    "text": "Approve"
                                ],
                                "style": "primary",
                                "value": "click_me_123"
                            ],
                            [
                                "type": "button",
                                "text": [
                                    "type": "plain_text",
                                    "emoji": true,
                                    "text": "Reject"
                                ],
                                "style": "danger",
                                "value": "click_me_123"
                            ]
                        ]				
			        ]
                ]

                slackSend(channel: "#general", blocks: blocks)

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
