def registry = 'https://evamp.jfrog.io'
def imageName = 'evamp.jfrog.io/evamp-docker-local/ttrend'
def version   = '2.1.2'
pipeline {
    agent{
		node {
			label 'maven'
		}
	}
environment {
	PATH = "/opt/apache-maven-3.9.5/bin:$PATH"
}

    stages {
        stage('build') {
            steps {
                sh 'mvn clean deploy'
            }
        }
		

        		

        stage(" Docker Build ") {
          steps {
            script {
               echo '<---------------- Docker Build Started --------------->'
               app = docker.build(imageName+":"+version)
               echo '<--------------- Docker Build Ends --------------->'
            }
          }
        }

                stage (" Docker Publish "){
            steps {
                script {
                   echo '<--------------- Docker Publish Started --------------->'  
                    docker.withRegistry(registry, 'artifact-cred-2'){
                        app.push()
                    }    
                   echo '<--------------- Docker Publish Ended --------------->'  
                }
            }
        }
		
		stage (" Deploy "){
			steps {
				script {
					sh './deploy.sh'
				}
			}
		}
		
    
  }
  
}
