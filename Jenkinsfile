pipeline {
    parameters {
        choice(name: 'PLATFORM_FILTER', choices: ['master', 'akali'], description: 'Run on specific platform')
    }
    agent none
    stages {
    	stage('Build_Stage and Test_Stage') {
    	matrix {
    		agent {
    			label "${PLATFORM}"
    		}
    		when { anyOf {
                expression { params.PLATFORM_FILTER == 'master' }
                expression { params.PLATFORM_FILTER == env.PLATFORM }
            } }
            axes {
                axis {
                    name 'PLATFORM'
                    values 'master', 'akali'
                }
                axis {
                    name 'APPS'
                    values 'nodejs', 'maven'
                }
            }
            excludes {
                exclude {
                    axis {
                        name 'PLATFORM'
                        values 'akali'
                        }
                    axis {
                        name 'APPS'
                        values 'nodejs'
                    }
                }
            }
            stages {
                stage('Build') {
                    steps {
                        echo "Do Build for ${PLATFORM} - ${APPS}"
                        }
                    }
                stage('Test') {
                    steps {
                        echo "Do Test for ${PLATFORM} - ${APPS}"
                    }
                }
            }
    	}
    	}
    }
}