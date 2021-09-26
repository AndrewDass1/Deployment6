pipeline{
	agent any
	
	tools {nodejs "node"}
	
	stages {
		stage ('Build') {
			steps {
			
			sh '''
				npm install
				npm run build
				sudo npm install -g serve
				serve -s build
			   '''
			}
		}
		
		stage('test') {
		agent {
			label 'a1'
		}
			steps{
			sh '''
			   npm install cypress
			   npm install mocha
			   npx cypress run --spec \
			./cypress/intregration/test.spec.js
			'''
		}
		post {
			always {
				junit 'results/cypress-report.xml'
			}
		}
	}	
	}
}


