pipeline {
    parameters {
        choice(name: 'PLATFORM_FILTER', choices: ['all', 'master', 'akali', 'ubuntu18-digitalocean'], description: 'Run on specific platform')
    }
    agent none
    stages {
    	matrix {
    		agent {
    			label '${PLATFORM}'
    		}
    		when { anyOf {
                expression { params.PLATFORM_FILTER == 'all' }
                expression { params.PLATFORM_FILTER == env.PLATFORM }
            } }
            axes {
                axis {
                    name 'PLATFORM'
                    values 'master', 'akali', 'ubuntu18-digitalocean'
                }
                axis {
                    name 'BROWSER'
                    values 'firefox', 'chrome', 'safari', 'edge'
                }
            }
            excludes {
                exclude {
                    axis {
                        name 'PLATFORM'
                        values 'akali'
                        }
                    axis {
                        name 'BROWSER'
                        values 'safari'
                    }
                }
            }
            stages {
                stage('Build') {
                    steps {
                        echo "Do Build for ${PLATFORM} - ${BROWSER}"
                        }
                    }
                stage('Test') {
                    steps {
                        echo "Do Test for ${PLATFORM} - ${BROWSER}"
                    }
                }
            }
    	}
    }
}