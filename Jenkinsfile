pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID     = credentials('AKIAW45YMRGH7YTQN346')
        AWS_SECRET_ACCESS_KEY = credentials('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')
        AWS_DEFAULT_REGION    = 'us-east-1'
        NETWORK_STACK_NAME    = 'P1'
        SSM_STACK_NAME        = 'P1-ssm-role'         
        WEBAPP_STACK_NAME     = 'P1-webapp'
        DATABASE_STACK_NAME   = 'P1-database'
        NETWORK_TEMPLATE_FILE = 'p1-network-1.yml'
        SSM_TEMPLATE_FILE     = 'p1-ssm-session-manager.yml'       
        WEBAPP_TEMPLATE_FILE  = 'p1-app-.yml'
        DATABASE_TEMPLATE_FILE= 'p1-db.yml' 
        NETWORK_PARAMETER_FILE= 'network-parameters.json' 
        WEBAPP_PARAMETER_FILE = 'webapp-parameters.json' 
        DATABASE_PARAMETER_FILE= 'database-parameters.json' 

    stages {
        stage('Deploy Network Stack') {
            steps {
                script {
                    // Validate network CloudFormation template
                    sh "aws cloudformation validate-template --template-body file://$NETWORK_TEMPLATE_FILE"
                    // Create or update network CloudFormation stack
                    sh "aws cloudformation deploy --stack-name $NETWORK_STACK_NAME --template-file $NETWORK_TEMPLATE_FILE --parameter-overrides file://$NETWORK_PARAMETER_FILE --capabilities CAPABILITY_IAM"
                }
            }
        }