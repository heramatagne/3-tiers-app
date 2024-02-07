pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION    = 'us-east-1'
        NETWORK_STACK_NAME    = 'P1'
        SSM_STACK_NAME        = 'P1-ssm-role'         
        WEBAPP_STACK_NAME     = 'P1-webapp'
        DATABASE_STACK_NAME   = 'P1-database'
        NETWORK_TEMPLATE_FILE = 'p1-network-1.yml'
        SSM_TEMPLATE_FILE     = 'p1-ssm-session-manager.yml'       
        WEBAPP_TEMPLATE_FILE  = 'p1-app-.yml'
        DATABASE_TEMPLATE_FILE= 'p1-db.yml' 

    }

    stages {
        stage('Deploy SSM Stack') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding', 
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    credentialsId: 'admin',
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    // Create or update network CloudFormation stack
                    sh "aws cloudformation deploy --stack-name $SSM_STACK_NAME --template-file $SSM_TEMPLATE_FILE"
                }
            }
        }
    }
}
