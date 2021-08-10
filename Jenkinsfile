pipeline {
    agent any
	tools { 
        maven 'MAVEN_HOME'  
    }

    stages {
			stage('Build') {
			environment{
			 scannerHome = tool 'sonarqube scanner'
			}
            steps {
                    bat("${scannerHome}/bin/sonar-scanner")
                
            }
        }
		
        stage('CompileandPackage') {
            steps {
			script{
			withSonarQubeEnv('sonarqubetest'){
				bat("mvn -Dmaven.test.failure.ignore sonar:sonar Dsonar.scanner.dumpToFile=D:\\Softwares\\ -Dsonar.login=64ff722206f9599e63b429194cda2239d673c5fa -Dsonar.projectKey=github-jenkins-java-sonar -Dsonar.host.url=http://localhost:9000/")
			}
            }
			}
        }
		
		stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
        }
        
    }
}