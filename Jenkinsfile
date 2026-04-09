pipeline {
    agent any

    parameters {
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Select action')
    }

    stages {

        stage('Run Terraform') {
            steps {
                git branch: 'main', url: 'https://github.com/PRATHAMKUKUDKAR/Terraform-GitHubAction.git'

                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-cred'
                ]]) {
                    sh '''
                    terraform init
                    terraform plan

                    if [ "$ACTION" = "apply" ]; then
                        terraform apply -auto-approve
                    else
                        terraform destroy -auto-approve
                    fi
                    '''
                }
            }
        }

    }
}
