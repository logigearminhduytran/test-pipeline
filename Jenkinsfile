def boolean test_results = false
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git branch: 'sample-demo', credentialsId: 'demo-kotlin-gradle-rest-api', url: 'https://github.com/LGVNJP-Demo/demo-kotlin-gradle-rest-api'
            }
        }
        stage('Run demo-kotlin-gradle-rest-api') {
            steps{
                gitHubPRStatus githubPRMessage('${GITHUB_PR_COND_REF} run started')
                echo "AAAAAA"
                script { test_results = true }
                echo "current stage status: $test_results"
            }
        }
        stage('Run demo-postman-test-automation if rest api successful') {
            steps{
                    script {
                        if (test_results == true) {
                            echo 'PASSSSS'
                            build 'demo-postman-test-automation'
                        } else {
                            echo 'FAILLL'
                            script { test_results = false }
                        }
                    }
                }
            }
        }
        
    }

