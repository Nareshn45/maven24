pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/maven.git'
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
                sh 'scp /home/ubuntu/.jenkins/workspace/Declarativepipeline/webapp/target/webapp.war ubuntu@172.31.26.88:/var/lib/tomcat9/webapps/testapp.war'
            }
        }
        stage('ContinuousTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/Declarativepipeline/testing.jar'
            }
        }
         stage('ContinuousDelivery')
        {
            steps
            {
                input message: 'Waiting for approval form the DM!', submitter: 'hari'
                sh 'scp /home/ubuntu/.jenkins/workspace/Declarativepipeline/webapp/target/webapp.war ubuntu@172.31.16.215:/var/lib/tomcat9/webapps/prodapp.war'
            }
        }
    }
}
