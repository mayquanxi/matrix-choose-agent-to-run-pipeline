pipeline {
    parameters {
        choice(name: 'PLATFORM_FILTER', choices: ['host', 'node13'], description: 'Run on specific platform')
    }
    agent none
    stages {
    	stage('Build_Stage and Test_Stage') {
    	matrix {
    		agent {
    			label "${PLATFORM}"
    		}
    		when { anyOf {
                expression { params.PLATFORM_FILTER == 'host' }
                expression { params.PLATFORM_FILTER == env.PLATFORM }
            } }
            axes {
                axis {
                    name 'PLATFORM'
                    values 'host', 'node13'
                }
                axis {
                    name 'APPS'
                    values 'nodejs'
                }
            }
            stages {
                stage('Build') {
                    steps {
                        echo "Do Build for ${PLATFORM} - ${APPS}"
                        sh 'node --version'
                        sh 'ls -l'

                        }
                    }
                stage('Test') {
                    steps {
                        echo "Do Test for ${PLATFORM} - ${APPS}"
                        sh 'yarn --version'
                        sh 'ls -l'
                    }
                }
            }
    	}
    	}
    }
}