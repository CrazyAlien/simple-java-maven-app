pipeline{
	
	agent {
		docker {
			image 'maven:3-alpine'
			args '-v /root/.m2:/root/.m2'
		}
	}

	stages {

		stage('Build') {

			steps {
				
				sh 'mvn -B -DskipTests clean package'

			}

			post {

				success {

					echo 'Build foi um sucesso!!!'

					mail to: 'pedro-g-almeida@alticelabs.com',
						subject: "!!Build do simple java maven app!! ${currentBuild.fullDisplayName}",
						body: "Que bomba este jenkins! ${env.BUILD_URL}"

				}

			}
		}

		stage('Test') {

			steps {
				sh 'mvn test'
			}

			post {

				always {
					junit 'target/surefire-reports/*.xml'
				}
			}

		}

		stage('Deliver') {
			
			steps {

				sh './jenkins/scripts/deliver.sh'
			}

		}

	}

}