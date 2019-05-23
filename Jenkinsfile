pipeline {
    agent none
    options {
        skipStagesAfterUnstable()
    } 
    stages {
    	stage('Static Analysis') {
            agent {
                docker {
                    image 'clburlison/pylint'
                }
            }
            steps {
                sh 'pylint sources/calc.py || true'
            }
        }
<<<<<<< HEAD
        stage('Build') {
            agent {
                docker {
                    image 'python:2-slim'
                }
            }
            steps {
                sh 'python -m py_compile sources/add2vals.py sources/calc.py'
            }
        } 
=======
>>>>>>> bc8c21ac59e7564ec092e79f6bd0ec64a1bb4cb3
        stage('Test') {
            agent {
                docker {
                    image 'qnib/pytest'
                }
            }
            steps {
                sh 'py.test --verbose --junit-xml test-reports/results.xml sources/test_calc.py'
            }
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
        stage('Deliver') { 
            agent {
                docker {
                    image 'cdrx/pyinstaller-linux:python2' 
                }
            }
            steps {
                sh 'pyinstaller --onefile sources/add2vals.py' 
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals' 
                }
            }
        }
    }
}
