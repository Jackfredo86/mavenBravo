pipeline
{
    agent any
    stages
    {
        stage('ContinuousDownload_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                         git 'https://github.com/Jackfredo86/maven123.git'
                    }
                    catch(Exception e1)
                    {
                        mail bcc: '', body: 'Jenkins is unable to downlooad the dev code from github', cc: '', from: '', replyTo: '', subject: 'Download failed', to: 'git.team@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousBuild_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                         sh 'mvn package'
                    }
                    catch(Exception e2)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code.', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'developers.team@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDeployment_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '2991e159-199e-4237-9d1f-70609156ad52', path: '', url: 'http://172.31.92.105:8080')], contextPath: 'testapp', war: '**/*.war'
                    }
                    catch(Exception e3)
                    {
                        mail bcc: '', body: 'Jenkins is unable to create an artifact from the downloaded code.', cc: '', from: '', replyTo: '', subject: 'Build Failed', to: 'developers.team@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousTesting_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                        sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
                    }
                    catch(Exception e4)
                    {
                        mail bcc: '', body: 'Selenium test scripts are failing', cc: '', from: '', replyTo: '', subject: 'Testing Failed', to: 'qa.team@gmail.com'
                        exit(1)
                    }
                }
            }
        }
        stage('ContinuousDelivery_Master')
        {
            steps
            {
                script
                {
                    try
                    {
                        deploy adapters: [tomcat9(credentialsId: '2991e159-199e-4237-9d1f-70609156ad52', path: '', url: 'http://172.31.84.240:8080')], contextPath: 'prodapp', war: '**/*.war'
                    }
                    catch(Exception e5)
                    {
                        mail bcc: '', body: 'Jenkins is unable to deploy into tomcat on the prodserver', cc: '', from: '', replyTo: '', subject: 'Delivery Failed', to: 'delivery.team@gmail.com'
                    }
                }
            }
        }
    }
}

