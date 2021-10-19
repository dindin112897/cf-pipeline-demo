@Library('shared-library') _
pipeline {
    agent any
	
	environment {
	    AWS_REGION = 'us-east-1'
            bucketName = "test-cf-bucket-geraldine"
			stackFileName = "wp.yaml"
			VpcId = "vpc-0c0aaa01e7b925bed"
			PubSub1 = "subnet-078cf6ab4e3ea4c9b"
			PubSub2 = "subnet-0f21467dcba8e1aad"
    }
	
	parameters { 
		string(
			name: 'ENV', 
			defaultValue: 'DEV', 
			description: 'Please insert the environment'
			)
		string(
			name: 'stackName', 
			defaultValue: 'myStack', 
			description: 'Please insert the stack name'
			)
	}
	
    stages {
     
		stage("Push template to S3") {
			steps {
				uploadFilesToS3(stackFileName: "${stackFileName}", workingDir: "${env.WORKSPACE}/stack_templates", bucketName: "${bucketName}")
			}
		}
		stage('Deploy Stack') {                  
                steps {
                    deploy_stack(stackName: "${stackName}", bucketName: "${bucketName}", stackFileName: "${stackFileName}", env: "${ENV}", VpcId: "${VpcId}", PublicSubnet1: "${PubSub1}", PublicSubnet2: "${PubSub2}")
                }
            }
		
		  
    }
   }
