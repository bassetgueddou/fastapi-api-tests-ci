pipeline {
    triggers { 
        upstream(upstreamProjects: 'fastapi-cicd', threshold: hudson.model.Result.SUCCESS) 
    }

    agent {
        docker {
            image 'postman/newman'
            args '--entrypoint=""'
        }
    }

    stages {
        stage('Check Newman Version') {
            steps {
                sh 'newman -v'
            }
        }

        stage('API Tests exec') {  
            steps {
                dir('tests') {
                    sh 'ls -R'
                    sh 'newman run collection.json -r cli,junit --reporter-junit-export="newman-report.xml"'
                }
            }
        }
    }

    post {
        always {
            sh 'ls -l tests/'
            junit 'tests/newman-report.xml' 
        }
    }
}
