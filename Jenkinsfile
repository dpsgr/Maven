pipeline
{
    agent any
    stages
    {
        stage('cont-download')
        {
            steps
            {
                git 'https://github.com/dpsgr/Maven.git'
            }
        }
        stage('cont-build')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('cont-deploy')
        {
            steps
            {
              deploy adapters: [tomcat9(credentialsId: 'cf87e01f-fcce-47f2-882d-bf5ddf77f495', path: '', url: 'http://172.31.45.47:8080')], contextPath: 'testapp', war: '**/*.war'
            }
        }
         stage('cont-test')
        {
            steps
            {
              git 'https://github.com/dpsgr/Functional-Testing.git'
              sh label: 'newapp.war', script: 'java -jar /var/lib/jenkins/workspace/Devjob/testing.jar'
            }
        }
         stage('cont-delivery')
        {
            steps
            {
                input message: 'Hello need your approval', submitter: 'DM'
            }
        }
    }
