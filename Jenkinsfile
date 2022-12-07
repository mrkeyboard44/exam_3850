/// Matthew Dandar, Dec 7 2022, Python Pipeline
/// BUILD: Installs Requirements
/// CODE QUALITY: tests code quality with pylint
/// CODE QUANTITY: counts amount of python files.
/// RUN TARGET: Runs main.py with 4 series of parameters
/// PACKAGE: returns files packaged in a zip file 

pipeline {
	    agent any
        parameters {
			string(defaultValue: 'do_nothing', description: 'Run Target Scripts', name: 'TARGET')
		}
	    stages {
			stage('Build') {
				steps {
                    echo 'Pipeline built by Matthew Dandar A01180450'
                    echo 'Installing The Requiremnts'
					sh 'pip install -r requirements.txt'
				}
				
			}
			stage('Code Quality') {
				steps {
					sh 'pylint-fail-under --fail_under 5.0 *.py'
				}

			}
            stage('Code Quantity') {
                steps {
                    echo "Counting the amount of python files in project"
                    script {
							FILE_AMOUNT = sh (
								script: 'ls *.py | wc -l',
								returnStdout: true
							)
							println FILE_AMOUNT
						}
                    echo 'ls | wc -l'
                }
            }
			stage('Run Target') {
                when {
                    expression { return params.TARGET == 'run' }
                }
				steps {
                    sh 'python3 main.py phone text output'
                    sh 'python3 main.py tablet csv output'
                    sh 'python3 main.py laptop json output'
                    sh 'python3 main.py phone yaml output'
                    sh 'ls output*'
				}

			}
			stage('Package'){
				steps {
					sh 'zip -r app.zip *.py'
					archiveArtifacts artifacts: 'app.zip'
                    echo 'By Matthew Dandar A01180450'
				}
			}
			
	    
		}
	    
	}