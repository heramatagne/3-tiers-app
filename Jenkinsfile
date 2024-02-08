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
        WEBAPP_PARAMETER_FILE = 'webapp-parameters.yml' 
        // MasterUsername        = '/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2'
        // MasterUserPassword    = 't2.micro'
        // DBName                = 'heramatagne@gmail.com'
    }

    stages {
        stage('Deploy Network Stack') {
            steps {
                sh "aws cloudformation deploy --stack-name $NETWORK_STACK_NAME --template-file $NETWORK_TEMPLATE_FILE"
            }
        }

        stage('Deploy SSM Stack') {
            steps {
                sh "aws cloudformation deploy --stack-name $SSM_STACK_NAME --template-file $SSM_TEMPLATE_FILE --capabilities CAPABILITY_IAM"
            }
        }

        stage('Deploy WebApp Stack') {
            steps {
                sh "aws cloudformation deploy --stack-name $WEBAPP_STACK_NAME --template-file $WEBAPP_TEMPLATE_FILE"
            }
        }
    // stages {
    //     stage('Deploy database') {
    //         steps {
    //             sh "aws cloudformation deploy --stack-name $DATABASE_STACK_NAME --template-file $DATABASE_TEMPLATE_FILE"
    //         }
    //     }       
    }
}
