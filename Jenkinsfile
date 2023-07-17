//def modules = [:]
pipeline {
    agent any

    //tools {
    //    maven 'maven_home'
    //}

    stages {
        //   stage('Load common-pipeline script') {
        //       steps {
        // //          script{
        // //              modules.first = load "common-pipeline.groovy"
        // //              modules.second = load "second.groovy"
        // //              modules.second.init(modules.first)
        // //              modules.first.test1()
        // //              modules.second.test2()
        // //              //modules.third.test3()
        // //         }
        //         checkout([$class: 'GitSCM',
        //             branches: [[name: 'master']],
        //             userRemoteConfigs: [[credentialsId: 'Multiple-repos-commits-with-one-pipeline',
        //             url: 'https://github.com/Rajugithub1989/Common-Pipeline.git']]])
        //             load 'common-pipeline.groovy'
        //      }
        //  }

        // // stage('Checkout java-hello-world-webapp-1') {
        // //     steps {
        // //         checkout([$class: 'GitSCM',
        // //             branches: [[name: 'master']],
        // //             userRemoteConfigs: [[credentialsId: 'Multiple-repos-commits-with-one-pipeline',
        // //             url: 'https://github.com/Rajugithub1989/java-hello-world-webapp-1.git']]])
        // //     }
        // // }

        stage("Checking Triggered Repo"){
            steps {
                script {
                    def commit = checkout scm
                    // we set BRANCH_NAME to make when { branch } syntax work without multibranch job
                    env.BranchName = commit.GIT_BRANCH.replace('origin/', '')

                    //actually build ....
                    echo "Got this branch Name : " + env.BranchName
                }
            }    
        } // Check stage 

        stage('Call groovy script') {
            steps {
                script {
            sh 'ls -lhrt'

            def rootDir = pwd()
            println("Current Directory: " + rootDir)
            def externalMethod = load "${rootDir}/common-pipeline.groovy"
            externalMethod.firstTest()
            }
        }
    }
// //         stage('Build-all-targets-in-parallel'){

// //           //def workspace = pwd()
// //           //echo workspace
// //           parallel(
// //             'first-parallel-target' :
// //              {
// //                 // Load the file 'file1.groovy' from the current directory, into a variable called "externalMethod".
// //                 //callScriptOne()
// //                 def externalMethod = load("common-pipeline.groovy")
// //                 // Call the method we defined in file1.
// //                 externalMethod.firstTest()
// //              }
// //           )
// //  }



        stage('Build and Test') {
             steps {
    // //             dir('java-hello-world-webapp-1') {
    // //                 checkout([$class: 'GitSCM',
    // //                           branches: [[name: 'master']],
    // //                           userRemoteConfigs: [[credentialsId: 'Multiple-repos-commits-with-one-pipeline',
    // //                                                url: 'https://github.com/Rajugithub1989/java-hello-world-webapp-1.git']]])

                     sh 'mvn clean test -PrunIndividualSuite -DsuiteXmlFile=Functional.xml -Denv=qa'

                 }
             }
    // //     }


    
    }

    post {
    always {

        echo "Job name: ${JOB_NAME}" 
        echo "Build number: ${BUILD_NUMBER}"
        echo "Build URL: ${BUILD_URL}" 


    }
}

}