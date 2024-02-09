pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION    = 'us-east-1'
        NETWORK_STACK_NAME    = 'P1'
        SSM_STACK_NAME        = 'P1-ssm-role'
        WEBAPP_STACK_NAME     = 'P1-webapp'
        NETWORK_TEMPLATE_FILE = 'p1-network-1.yml'
        SSM_TEMPLATE_FILE     = 'p1-ssm-session-manager.yml'
        WEBAPP_TEMPLATE_FILE  = 'p1-app.yml'
        WEBAPP_PARAMETER_FILE = 'webapp-parameters.yml'
        OperatorEMail = sh(script: 'aws ssm get-parameter --region $AWS_DEFAULT_REGION --name /p1/webapp/peratorEMail --query "Parameter.Value" --output text', returnStdout: true).trim()
    }

    stages {
        stage('Get Operator Email') {
            steps {
                script {
                    OperatorEMail = OperatorEMail.trim() // Trim whitespace
                    // Validate email address format using regular expression
                    if (!(OperatorEMail =~ /[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/)) {
                        error "Invalid email address format: $OperatorEMail"
                    }
                }
            }
        }

        stage('Deploy Network Stack') {
            steps {
                sh "aws cloudformation deploy --stack-name $NETWORK_STACK_NAME --template-file $NETWORK_TEMPLATE_FILE --region $AWS_DEFAULT_REGION"
            }
        }

        stage('Deploy SSM Stack') {
            steps {
                sh "aws cloudformation deploy --stack-name $SSM_STACK_NAME --template-file $SSM_TEMPLATE_FILE --capabilities CAPABILITY_IAM --region $AWS_DEFAULT_REGION"
            }
        }

        stage('Deploy WebApp Stack') {
            steps {
                sh "aws cloudformation deploy --stack-name $WEBAPP_STACK_NAME --template-file $WEBAPP_TEMPLATE_FILE --parameter-overrides OperatorEMail=$OperatorEMail --region $AWS_DEFAULT_REGION"
            }
        }
    }
}
