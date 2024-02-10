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
        WEBAPP_TEMPLATE_FILE  = 'p1-app.yml'  // Corrected the template file name
        DATABASE_TEMPLATE_FILE= 'p1-db.yml'
        WEBAPP_PARAMETER_FILE = 'webapp-parameters.yml'
        OperatorEMail         = sh(script: 'aws ssm get-parameter --region us-east-1 --name /p1/webapp/peratorEMail --query "Parameter.Value" --output text', returnStdout: true).trim()        
    }

    stages {
        // stage('Deploy Network Stack') {
        //     steps {
        //         sh "aws cloudformation deploy --stack-name $NETWORK_STACK_NAME --template-file $NETWORK_TEMPLATE_FILE --region $AWS_DEFAULT_REGION"
        //     }
        // }

        // stage('Deploy SSM Stack') {
        //     steps {
        //         sh "aws cloudformation deploy --stack-name $SSM_STACK_NAME --template-file $SSM_TEMPLATE_FILE --capabilities CAPABILITY_IAM --region $AWS_DEFAULT_REGION"
        //     }
        // }

        stage('Deploy WebApp Stack') {
            steps {
                sh "aws cloudformation deploy --stack-name $WEBAPP_STACK_NAME --template-file $WEBAPP_TEMPLATE_FILE --parameter-overrides OperatorEMail=$OperatorEMail --region $AWS_DEFAULT_REGION"
            }
        }

        // stage('Deploy database') {
        //     steps {
        //         sh "aws cloudformation deploy --stack-name $DATABASE_STACK_NAME --template-file $DATABASE_TEMPLATE_FILE --region $AWS_DEFAULT_REGION"
        //     }
        // }       
    }
}
