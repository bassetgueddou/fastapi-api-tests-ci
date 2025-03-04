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
        stage('API Tests exec') {  
            steps {
                dir('tests') {
                    sh 'newman run collection.json -r cli,junit --reporter-junit-export="newman-report.xml"'
                }
            }
        }
    }

    post {
        always {
            junit 'tests/newman-report.xml' 
        }
    }
}
