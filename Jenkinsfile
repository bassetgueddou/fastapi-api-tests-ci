pipeline {
    agent {
        docker {
            image 'postman/newman'
            args '--entrypoint=""'
        }
    }

        stage('API Tests exec') {
            steps {
                dir('tests') {
                    sh 'newman run collections/collection.json -r cli,junit --reporter-junit-export="newman-report.xml"'
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