pipeline
{
    agent { label 'myslave'}
    stages{
        stage('continuous download')
        {
            steps{
               git 'https://github.com/intelliqittrainings/maven.git'
            }
        }
        stage('continuous build')
        {
            steps{
                sh 'mvn package'
            }
        }
        stage('continous deploy')
        {
            steps{
              deploy adapters: [tomcat9(credentialsId: 'd4f4e493-2098-4473-ac94-fb2ca43e4701', path: '', url: 'http://172.31.28.46:8080')], contextPath: 'qaapp', onFailure: false, war: '**/*.war'  
            }
        }
        stage('continous testing')
        {
            steps{
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                 sh 'java -jar /home/ubuntu/remote_root/workspace/Declarativepipeline/testing.jar'
            }
        }
        stage('continous delivery')
        {
            steps{
              deploy adapters: [tomcat9(credentialsId: 'd4f4e493-2098-4473-ac94-fb2ca43e4701', path: '', url: 'http://172.31.28.255:8080')], contextPath: 'qaapp', onFailure: false, war: '**/*.war'    
            }
        }
    }
}
