pipeline{
    agent{
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-v /root/.m2:/root/.m2'
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages{
        stage("Build"){
            steps{
                echo "========Building Java Project========"
                sh 'mvn -B -DskipTests clean package'
            }
            post{
                always{
                    echo "========always========"
                }
                success{
                    echo "========Build executed successfully========"
                }
                failure{
                    echo "========Build execution failed========"
                }
            }
        }

        stage("Test"){
            steps{
                echo "========running test========"
                sh 'mvn test'
            }
            post{
                always{
                    echo "========always========"
                    junit "target/surefire-reports/*.xml"
                }
                success{
                    echo "========Test executed successfully========"
                }
                failure{
                    echo "========Test execution failed========"
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "====++++executing Deploy++++===="
                sh './jenkins/scripts/deliver.sh'
            }
            post{
                always{
                    echo "====++++always++++===="
                }
                success{
                    echo "====++++Deploy executed successfully++++===="
                }
                failure{
                    echo "====++++Deploy execution failed++++===="
                }
        
            }
        }

    }

    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}