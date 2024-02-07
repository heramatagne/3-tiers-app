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
        LatestAmiId           = '/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2'
        InstanceType          = 't2.micro'
        OperatorEMail         = 'heramatagne@gmail.com'
    }

    stages {
        stage('Deploy Network Stack') {
            steps {
                // withCredentials([[
                    // $class: 'AmazonWebServicesCredentialsBinding', 
                    // accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    // credentialsId: 'admin',
                    // secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                    // Create or update network CloudFormation stack
                    sh "aws cloudformation deploy --stack-name $NETWORK_STACK_NAME --template-file $NETWORK_TEMPLATE_FILE"
                }
            }
        }

//         stage('Deploy SSM Stack') {
//             steps {
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding', 
//                     accessKeyVariable: 'AWS_ACCESS_KEY_ID',
//                     credentialsId: 'admin',
//                     secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
//                     // Create or update SSM CloudFormation stack with CAPABILITY_IAM
//                     sh "aws cloudformation deploy --stack-name $SSM_STACK_NAME --template-file $SSM_TEMPLATE_FILE --capabilities CAPABILITY_IAM"
//                 }
//             }
//         }

//         stage('Deploy WebApp Stack') {
//             steps {
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding', 
//                     accessKeyVariable: 'AWS_ACCESS_KEY_ID',
//                     credentialsId: 'admin',
//                     secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
//                     // Create or update WebApp CloudFormation stack with CAPABILITY_IAM and parameter overrides
//                     sh "aws cloudformation deploy --stack-name $WEBAPP_STACK_NAME --template-file $WEBAPP_TEMPLATE_FILE --parameter-overrides LatestAmiId=$LatestAmiId InstanceType=$InstanceType OperatorEMail=$OperatorEMail --capabilities CAPABILITY_IAM"
//                 }
//             }
//         }
    // }
}
