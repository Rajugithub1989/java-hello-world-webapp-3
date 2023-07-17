pipeline {
    agent any

    tools {
        maven 'maven_home'
    }

    stages {
        // stage('Load common-pipeline script') {
        //     steps {
        //         checkout([$class: 'GitSCM',
        //             branches: [[name: 'master']],
        //             userRemoteConfigs: [[credentialsId: 'Multiple-repos-commits-with-one-pipeline',
        //             url: 'https://github.com/Rajugithub1989/Common-Pipeline.git']]])
        //             load 'common-pipeline.groovy'
        //     }
        // }

        stage('Checkout java-hello-world-webapp-3') {
            steps {
                checkout([$class: 'GitSCM',
                    branches: [[name: 'master']],
                    userRemoteConfigs: [[credentialsId: 'Multiple-repos-commits-with-one-pipeline',
                    url: 'https://github.com/Rajugithub1989/java-hello-world-webapp-3.git']]])
            }
        }


        // stage('Checkout kine-alert-deliver') {
        //     steps {
        //         checkout([$class: 'GitSCM',
        //             branches: [[name: 'development']],
        //             userRemoteConfigs: [[credentialsId: '164c73e9-36dc-47a1-816c-9026492b1e99',
        //             url: 'https://github.com/kine-admin/kine-alert-deliver.git']]])
        //     }
        // }


        // stage('Checkout kine-alert-generate') {
        //     steps {
        //         checkout([$class: 'GitSCM',
        //             branches: [[name: 'development']],
        //             userRemoteConfigs: [[credentialsId: '164c73e9-36dc-47a1-816c-9026492b1e99',
        //             url: 'https://github.com/kine-admin/kine-alert-generate.git']]])
        //     }
        // }

       stage('Build and Test') {
            steps {
                dir('java-hello-world-webapp-3') {
                    checkout([$class: 'GitSCM',
                              branches: [[name: 'master']],
                              userRemoteConfigs: [[credentialsId: 'Multiple-repos-commits-with-one-pipeline',
                                                   url: 'https://github.com/Rajugithub1989/java-hello-world-webapp-3.git']]])

                    sh 'mvn clean test -PrunIndividualSuite -DsuiteXmlFile=Functional.xml -Denv=qa'

                }
            }
        }


        post {
           always {
              //echo "Result: ${BUILD_RESULT}" 
              //echo "Output: ${BUILD_OUTPUT}"
               echo "Job name: ${JOB_NAME}" 
               echo "Build number: ${BUILD_NUMBER}"
               echo "Build URL: ${BUILD_URL}" 
              //echo "Duration: ${duration}" 


       // archiveArtifacts artifacts: 'job_data.txt', onlyIfSuccessful: false
    }
  }
}

    // post {
    //     failure {
    //         mail to: 'sanjeev.ks@kine.ai, pooja.b@kine.ai',
    //              cc: 'ravikumarsv@kine.ai',
    //              subject: "FAILED: Build ${env.JOB_NAME}",
    //              body: "Build failed ${env.JOB_NAME} build no: ${env.BUILD_NUMBER}.\n\nView the log at:\n${env.BUILD_URL}\n\nReports URL: http://44.214.170.120/Reports/"
    //     }
    //     success {
    //         mail to: 'sanjeev.ks@kine.ai, pooja.b@kine.ai',
    //              cc: 'ravikumarsv@kine.ai',
    //              subject: "SUCCESSFUL: Build ${env.JOB_NAME}",
    //              body: "Build Successful ${env.JOB_NAME} build no: ${env.BUILD_NUMBER}\n\nView the log at:\n${env.BUILD_URL}\n\nReports URL: http://44.214.170.120/Reports/"
    //     }
    //     aborted {
    //         mail to: 'sanjeev.ks@kine.ai, pooja.b@kine.ai',
    //              cc: 'ravikumarsvkine.ai',
    //              subject: "ABORTED: Build ${env.JOB_NAME}",
    //              body: "Build was aborted ${env.JOB_NAME} build no: ${env.BUILD_NUMBER}\n\nView the log at:\n${env.BUILD_URL}\n\nReports URL: http://44.214.170.120/Reports/"
    //     }
    // }
}