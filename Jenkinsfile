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
    
    } 
 }
