pipeline {
    agent any
    triggers {
        GenericTrigger(
            genericVariables: [
                [key: 'name', value: '$.pusher.name'],                
                [key: 'url', value: '$.commits.[0].url'],
		[key: 'branch', value: '$.repository.master_branch'],
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
				    "text": "${name} made commit to ${branch}, please accept it."
                            ]
                        ],
                        [
			    "type": "section",
			    "text": [
				"type": "mrkdwn",
                               	"text": "You can see all changes *<${url}|here>*"
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
                    input id: 'confirm', message: 'Proceed?', ok: 'Accept', submitter: 'admin'
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
