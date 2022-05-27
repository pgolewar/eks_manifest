pipeline{
    agent any
    environment {
        AWS_ACCOUNT_ID="273488666711"
        AWS_DEFAULT_REGION="us-east-1" 
        IMAGE_REPO_NAME="coit_repository"
        IMAGE_TAG="latest"
        REPOSITORY_URI = "${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_DEFAULT_REGION}.amazonaws.com/${IMAGE_REPO_NAME}"
                 }
	stages{
		stage('Checkout'){
			steps{
				sh 'mvn --version'
				sh 'docker --version'
				echo "Build"
				echo "PATH - $PATH"
				echo "BUILD_NUMBER - $env.BUILD_NUMBER"
				echo "BUILD_ID - $env.BUILD_ID"
				echo "BUILD_TAG - $env.BUILD_TAG"
				echo "JOB_NAME - $env.JOB_NAME"
			}
		}
        
	/* stage('Build '){
            steps{
                dir('./coit-frontend'){
				echo "path- $PATH"
				script{
				def FRONTENDDOCKER = 'Dockerfile-multistage'
				DockerFrontend = docker.build("eks_manifest/coit-frontend:${env.BUILD_TAG}","-f ${FRONTENDDOCKER} .")
				//sh('docker build -t kollidatta/coitfrontend:v1 -f Dockerfile-multistage .')
				}
				} 
            }
        }
	*/			
            
        
		stage('Push Frontend'){
			steps{
				sh 'https://docs.docker.com/engine/reference/commandline/login/#credentials-store'
				sh 'docker tag coit-frontend 273488666711.dkr.ecr.us-east-1.amazonaws.com/coit_repository'
				 sh 'docker push 273488666711.dkr.ecr.us-east-1.amazonaws.com/coit_repository'

			}
		}
		
    }
	post {
			always{
				echo "Im awesome. I run always"
			}
			success{
				echo 'I run when you are successful'
			}
			failure{
				echo 'I run when you fail'
			}
		}
	

}


