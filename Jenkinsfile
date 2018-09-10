pipeline {
    agent any
     tools {
        maven 'localMaven'
    }

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
                sh " sudo docker build . -t tomcatwebapp:${env.BUILD_ID}"
            }
            post {
                success {
                    echo 'Now Archiving...'


                }
            }
        }
	stage("publish to s3") {
            steps([
                $class: 'S3BucketPublisher',
                entries: [[
                    sourceFile: 'tomcatwebapp',
                    bucket: 'pawan979797',
                    selectedRegion: 'eu-east-1',
                    noUploadOnFailure: true,
                    managedArtifacts: true,
                    flatten: true,
                    showDirectlyInBrowser: true,
                    keepForever: true,
                ]],
                profileName: 'myprofile',
                dontWaitForConcurrentBuildCompletion: false, 
            ])
        }
		
    }
}
