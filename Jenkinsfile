pipeline {
	    agent any
        parameters {
			string(defaultValue: 'do_nothing', description: 'Run the App', name: 'TARGET')
		}
	    stages {
			stage('Build') {
				steps {
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
                    script {
							USAGE_REPORT = sh (
								script: 'ls | wc -l',
								returnStdout: true
							)
							println USAGE_REPORT
						}
                    sh 'ls | wc -l'
                }
            }
			stage('Run Target') {
				// steps {
				// 	script {
				// 		scriptDir = new File(getClass().protectionDomain.codeSource.location.path).parent
				// 		echo "$scriptDir"
				// 		sh 'rm -rfv *test-reports/*'
				// 		def files = findFiles(glob: "**/test_*.py")
				// 		for (file in files) {
				// 			def file_path = file.path
				// 			sh "coverage run --omit */site-packages/*,*/dist-packages/* $file_path"
				// 		}
				// 		sh 'coverage report'
				// 	}
				// }
                when {
                    expression { return params.TARGET == 'run' }
                }
				steps {
					// always {
					// 	script {
					// 		// def files = ['phone text', 'tablet csv]
					// 		for (file in files) {
					// 			def file_path = file.path
					// 			sh "python main.py"
					// 		}
					// 	}

					// }
                    sh 'python main.py phone text output'
                    sh 'python main.py tablet csv output'
                    sh 'python main.py laptop json output'
                    sh 'python main.py phone yaml output'
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