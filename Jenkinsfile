pipeline{
    agent any
    stages{
        stage("Checkout"){
            steps{
                echo "========executing checkout========"
                git url:"https://github.com/cloud-junction/devops-webapp-maven.git", branch:"master"
            }
                       
        }
        stage("Unit Test"){
            steps{
                sh "mvn test"
            }
        }
        
        stage("Build Package"){
            steps{
                sh "mvn package"
            }
        }
        
        stage("Approval"){
            steps{
                   timeout(time: 15, unit: 'MINUTES'){ 
	               input message: 'Do you approve deployment for production?' , ok: 'Yes'}
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
            mail to:"cloud.junction.in.3@gmail.com",
            subject: "Status of pipeline: ${currentBuild.fullDisplayName}",
            body: "${env.BUILD_URL} has result FAILURE "
        }
    }
}
