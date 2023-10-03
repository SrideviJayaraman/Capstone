pipeline {
    agent any
        stage('Terraform and Environment Variables') {
            steps {
                dir('Capstone/Infrastructure/Terraform_and_Ansible') {
                    script {
                        sh 'terraform init'
                        sh 'terraform plan -out=tfplan'
                        sh 'terraform apply -auto-approve tfplan'
                        
                        // Store Terraform outputs as environment variables
                        env.TF_VAR_output_instance_id = sh(script: 'terraform output -raw output_name_1', returnStdout: true).trim()
                        env.TF_VAR_output_public_ip = sh(script: 'terraform output -raw output_name_2', returnStdout: true).trim()
                        env.TF_VAR_output_private_ip = sh(script: 'terraform output -raw output_name_3', returnStdout: true).trim()

                        // Print the output values
                        echo "Instance id: ${env.TF_VAR_output_instance_id}"
                        echo "Public ip: ${env.TF_VAR_output_public_ip}"
                        echo "Private ip: ${env.TF_VAR_output_private_ip}"
                    }
                }
            }
        }
    }
}
