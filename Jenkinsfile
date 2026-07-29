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
               git branch: 'main', url: 'https://github.com/CloudTechDevOps/Terraform-0730am.git'
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

