pipeline {
    agent any
    parameters {
        choice choices: ['chrome', 'firefox'], description: 'Select Browser', name: 'BROWSER'
    }
    stages {
        stage("start grid") {
            steps {
                echo "======== executing (start grid) stage ========"
                bat  "docker-compose -f grid.yaml up --scale ${BROWSER}=2 -d"
            }
            post {
                success {
                    echo "======== (start grid) stage executed successfully ========"
                }
                failure {
                    echo "======== (start grid) stage execution failed ========"
                }
            }
        }
        stage("run test") {
            steps {
                echo "======== executing (run test) stage ========"
                bat  "docker-compose -f test-suites.yaml up"
            }
            post {
                success {
                    echo "======== (run test) stage executed successfully ========"
                }
                failure {
                    echo "======== (run test) stage execution failed ========"
                }
            }
        }
    }
    post {
        always {
            echo "======== bring containers down ========"
            bat  "docker-compose -f grid.yaml down"
            bat  "docker-compose -f test-suites.yaml down"
            echo "======== archiving output ========"
            archiveArtifacts artifacts: 'output/vendor-portal/emailable-report.html', followSymlinks: false
            archiveArtifacts artifacts: 'output/flight-reservation/emailable-report.html', followSymlinks: false
        }
        success {
            echo "======== pipeline executed successfully ========"
        }
        failure {
            echo "======== pipeline execution failed ========"
        }
        aborted {
            echo "======== pipeline execution aborted ========"
        }
    }
}