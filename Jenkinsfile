pipeline {
    agent any

    stages {
        stage('Terraform and Environment Variables') {
            steps {
                dir('Capstone/Infrastructure/Terraform_and_Ansible') {
                    script {
                        // Step 1: Initialize Terraform
                        sh 'terraform init'

                        // Step 2: Plan the Terraform changes
                        sh 'terraform plan -out=tfplan'

                        // Step 3: Apply the Terraform changes with auto-approve
                        sh 'terraform apply -auto-approve tfplan'
                        
                        // Step 4: Store Terraform outputs as environment variables
                        env.TF_VAR_output_instance_id = sh(script: 'terraform output -raw output_name_1', returnStdout: true).trim()
                        env.TF_VAR_output_public_ip = sh(script: 'terraform output -raw output_name_2', returnStdout: true).trim()
                        env.TF_VAR_output_private_ip = sh(script: 'terraform output -raw output_name_3', returnStdout: true).trim()

                        // Step 5: Print the output values
                        echo "Instance id: ${env.TF_VAR_output_instance_id}"
                        echo "Public ip: ${env.TF_VAR_output_public_ip}"
                        echo "Private ip: ${env.TF_VAR_output_private_ip}"
                    }
                }
            }
        }
    }
}
