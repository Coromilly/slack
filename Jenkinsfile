pipeline {
    agent any
    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'name', value: '$.commits..author.name.[]']
            ],

            causeString: 'Triggered by $name',

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
                script {
                    blocks = [
                        [
                            "type": "section",
                            "text": [
                                "type": "mrkdwn",
                                "text": "${name} made commit, please accept hit."
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
//                                     "url": "http://coromilly:11ab9572042c68809cbf56589831c9e322@18.207.112.223:8080/job/new1/37/input/Confirm/proceedEmpty"
                                    "url": "${BUILD_URL}/input/Confirm/proceedEmpty"
                                ],
                                [
                                    "type": "button",
                                    "text": [
                                        "type": "plain_text",
                                        "emoji": true,
                                        "text": "Reject"
                                    ],
                                    "style": "danger",
                                    "url": "${BUILD_URL}/input/Confirm/abort"
                                ]
                            ]				
                        ]
                    ]
                }
                
                slackSend(channel: "#devops", blocks: blocks)

                script {
                    input id: 'confirm', message: 'Proceeed?', ok: 'Yes', submitter: 'admin'
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
