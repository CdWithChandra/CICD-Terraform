pipeline {
    agent any

    stages {
        stage('first') {
            steps {
                echo 'Hello first stage'
            }
        }
    }
}

--------------------------
multi stage example:
-------------------------
pipeline {
    agent any

    stages {
        stage('first') {
            steps {
                echo 'Hello first stage'
            }
        }
        
        stage('second') {
            steps {
                echo 'Hello second stage'
            }
        }
    }


### With terraform examples ###


#Ex:-1

pipeline {
    agent any

    stages {
        stage('git checkout') {
            steps {
               git branch: 'main', url: 'https://github.com/CdWithChandra/Terraform_CICD.git'
            }
        }
         stage('init') {
            steps {
                sh '''
                     cd Day-1-Terraform-basic-config
                     terraform init
                     '''
                
            }
        }
        stage('plan') {
            steps {
                sh '''
                    cd Day-1-Terraform-basic-config
                    terraform plan
                    '''
            }
        }
        stage('apply') {
            steps {
                sh '''
                    cd Day-1-Terraform-basic-config
                    terraform apply -auto-approve
                    '''
            }
        }
    }
}

--------------------------
multi stage example: Ec2 
-------------------------

pipeline {
    agent any

    stages {
        stage('clone') {
            steps {
               git branch: 'main', url: 'https://github.com/CdWithChandra/Terraform_CICD.git'
            }
        }
        stage('init') {
            steps {
               sh 'terraform init'
            }
        }
        stage('validate') {
            steps {
               sh 'terraform validate'
            }
        }
        stage('plan') {
            steps {
               sh 'terraform plan'
            }
        }
        stage('approval') {
            steps {
               input(
                        message: 'Approve Terraform deployment?',
                        ok: 'Deploy'
                    )
            }
        }
        
        stage('apply') {
            steps {
               sh 'terraform apply -auto-approve'
            }
        }
        stage('destroy') {
            steps {
               sh 'terraform destroy -auto-approve'
            }
        }
    }
}

----------------------------------------------------------
multi stage with github repo change directory example: Ec2 
----------------------------------------------------------

pipeline {
    agent any

    stages {
        stage('Git-clone') {
            steps {
               git branch: 'main', url: 'https://github.com/CdWithChandra/terraform-practice.git'
            }
        }
        stage('terraform-init') {
            steps {
                dir('Day2-terraform-configurations') {
               sh 'terraform init'
            }
        }
    }
        stage('terraform-validate') {
            steps {
                dir('Day2-terraform-configurations') {
               sh 'terraform validate'
            }
        }
    }
        stage('terraform-plan') {
            steps {
                  dir('Day2-terraform-configurations') {
               sh 'terraform plan'
            }
        }
   }
        stage('Execute') {
            steps {
               input(
                        message: 'Approve Terraform deployment?',
                        ok: 'Deploy'
                    )
            }
        }
        
        stage('terraform-apply') {
            steps {
                dir('Day2-terraform-configurations') {
               sh 'terraform apply -auto-approve'
            }
        }
    }
        stage('terraform-destroy') {
            steps {
               sh 'terraform destroy -auto-approve'
            }
        }
    }
}    

----------------------------------------------------------
multi stage with choice Parameters example: Ec2 
----------------------------------------------------------
pipeline {
    agent any

    parameters {
        choice(
            name: 'ACTION',
            choices: ['Apply', 'Destroy'],
            description: 'Select the Terraform action'
        )
    }

    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/CdWithChandra/Terraform_CICD.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('Terraform Plan') {
            when {
                expression { params.ACTION == 'Apply' }
            }
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }

        stage('Approval') {
            steps {
                input(
                    message: "You selected ${params.ACTION}. Continue?",
                    ok: "Proceed"
                )
            }
        }

        stage('Execute') {
            steps {
                script {
                    if (params.ACTION == 'Apply') {
                        sh 'terraform apply -auto-approve tfplan'
                    } else {
                        sh 'terraform destroy -auto-approve'
                    }
                }
            }
        }
    }
}

----------------------------------------------------------------------
multi stage with choice Parameters with change directory example: Ec2 
----------------------------------------------------------------------
pipeline {
    agent any

    parameters {
        choice(
            name: 'ACTION',
            choices: ['Apply', 'Destroy'],
            description: 'Select the Terraform action'
        )
    }

    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/CdWithChandra/terraform-practice.git'
            }
        }

        stage('Terraform Init') {
            steps {
                dir('Day2-terraform-configurations') {
                sh 'terraform init'
            }
        }
   }
        stage('Terraform Plan') {
            when {
                expression { params.ACTION == 'Apply' }
            }
            steps {
                dir('Day2-terraform-configurations') {
                sh 'terraform plan -out=tfplan'
            }
        }
   }
        stage('Approval') {
            steps {
                input(
                    message: "You selected ${params.ACTION}. Continue?",
                    ok: "Proceed"
                )
            }
        }

        stage('Execute') {
            steps {
                script {
                    if (params.ACTION == 'Apply') {
                        dir('Day2-terraform-configurations') {
                        sh 'terraform apply -auto-approve tfplan'
                        }
                    } else {
                        sh 'terraform destroy -auto-approve'
                    }
                }
            }
        }
         stage('Terraform destroy') {
            steps {
                dir('Day2-terraform-configurations') {
                sh 'terraform destroy -auto-approve'
            }
            }
        }
    }
}
