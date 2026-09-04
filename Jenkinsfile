
pipeline {
    agent {
        label 'dev'
    }
    options {
        timeout( time: 1 , unit: 'HOURS' )
        disableConcurrentBuilds()
        ansiColor('xterm')
    }
    parameters {
        string(name: 'appVersion', defaultValue: '1.0.0', description: 'what is application version?')
        //choice(name: 'action', choices: ['Apply', 'Destroy'], description: 'Pick something')
    }
    environment {
        def appVersion = ''
        nexusUrl = 'nexus.lokesh.shop:8081'
    }
    stages {
        stage('print Version') {
            steps {
                script {
                    echo "application version : ${params.appVersion}"
                }
            }
        }
        stage('Init') {
            steps {
                sh """
                    cd terraform
                    terraform init -reconfigure
                """
            }
        }
        stage('Plan') {
            // when {
            //     expression {
            //         params.action == "Apply"
            //     }
            // }
            steps {
                sh """
                    pwd
                    cd terraform
                    terraform plan -var="app_version=${params.appVersion}" 
                """
            }
        }
        stage('Apply') {
            // when {
            //     expression {
            //         params.action == "Apply"
            //     }
            // }
            steps {
                sh """
                    cd terraform
                    terraform apply --auto-approve -var="app_version=${params.appVersion}" 
                """
            }
        }
        // stage('Destroy') {
            
        //     when {
        //         expression {
        //             params.action == "Destroy"
        //         }
        //     }
        //     steps {
        //         sh """
        //             cd terraform
        //             terraform destroy --auto-approve -var="app_version=${params.appVersion}" 
        //         """
        //     }
        // }
    }
        
    post {
        always {
            echo "it will run always"
            deleteDir()
        }
        success {
            echo "it will run when the pipeline is success"
        }
         failure {
            echo "it will run when pipeline is failure"
        }
    }
    
}