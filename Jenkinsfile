pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/naveenkumar10081995/maven.git'
            }
        }
        stage('ContinuousBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContinuousDeployment')
         {
            steps
            {
              deploy adapters: [tomcat9(credentialsId: '5b2397b3-b95a-4a34-93c4-6092e7f0ef89', path: '', url: 'http://172.31.22.65:8080')], contextPath: 'test', war: '**/*.war'     
            }
	}
        stage('ContinuousTesting')
        {
            steps
            {  
               git 'https://github.com/naveenkumar10081995/functional-testing.git'
	          sh 'java -jar /home/ubuntu/.jenkins/workspace/items/testing.jar'
            }
        }
       
    }
    
    post
    {
        success
        {
            input message: 'Need approval from the DM!', submitter: 'srinivas'
            deploy adapters: [tomcat9(credentialsId: 'ff0308f1-d148-44c6-9b2c-cab29c4c2fc8', path: '', url: 'http://172.31.16.239:8080')], contextPath: 'qa', war: '**/*.war'
	   }
        failure
        {
            mail bcc: '', body: 'Continuous Integration has failed', cc: '', from: '', replyTo: '', subject: 'CI Failed', to: 'selenium.saikrishna@gmail.com'
        }
       
    }
    
    
    
    
    
    
}
