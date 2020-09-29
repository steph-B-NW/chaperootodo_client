pipeline{
        agent any
	environment {
		app_version = 'v1'
	}
        stages{
            stage('Build Image'){
                steps{
			script{
				if (env.rollback == 'false'){
                    			image = docker.build("stephbnw/chaperoo-fronted")
				}
			}
                }
            }
            stage('Tag & Push Image'){
               steps{
                   script{
                       if (env.rollback == 'false'){
                           docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials;){
                               image.push("${.app_version}")
                                  }
                             }
                        }
                    }
                }
            stage('Deploy App'){
                steps{
                    sh "docker-compose pull && docker-compose up -d"
                }
            }
        }    
}
