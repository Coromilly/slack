sipipeline {
    agent any
    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'branch', value: '$.ref']
            ],

            causeString: 'Triggered on $ref',

            token: '12345',
            tokenCredentialId: '',

            printContributedVariables: true,
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
                                "text": "Hello, please accept my job."
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
                                        "text": "Approove"
                                    ],
                                    "style": "primary",
//                                     "url": "http://coromilly:11ab9572042c68809cbf56589831c9e322@18.207.112.223:8080/job/new1/37/input/Confirm/proceedEmpty"
                                    "url": "http://18.207.112.223:8080/job/new1/39/input/Confirm/proceedEmpty"
                                ],
                                [
                                    "type": "button",
                                    "text": [
                                        "type": "plain_text",
                                        "emoji": true,
                                        "text": "Reject"
                                    ],
                                    "style": "danger",
                                    "value": "click_me"
                                ]
                            ]				
                        ]
                    ]
                }
                
                slackSend(channel: "#devops", message: "Starting to build ${branch} for ${name}", blocks: blocks)

                script {
                    input id: 'confirm', message: 'Proceed?', ok: 'Yes', submitter: 'admin'
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
