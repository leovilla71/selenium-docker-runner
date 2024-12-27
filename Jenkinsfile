pipeline{
    agent any
    stages{
        stage("run test"){
            steps{
                echo "======== executing run test stage ========"
                bat  "docker-compose up"
            }
            post{
                success{
                    echo "======== run test stage executed successfully ========"
                }
                failure{
                    echo "======== run test stage execution failed ========"
                }
            }
        }
        stage("bring grid down"){
            steps{
                echo "======== executing bring grid down stage ========"
                bat  "docker-compose down"
            }
            post{
                success{
                    echo "======== bring grid down stage executed successfully ========"
                }
                failure{
                    echo "======== bring grid down stage execution failed ========"
                }
            }
        }
    }
    post{
        success{
            echo "======== pipeline executed successfully ========"
        }
        failure{
            echo "======== pipeline execution failed ========"
        }
        aborted{
            echo "======== pipeline execution aborted ========"
        }
    }
}