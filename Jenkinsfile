pipeline {
    agent any
    triggers {
    pollSCM '* * * * *'
    }

    stages {
      //  stage('Checkout') {
        //    steps {
          //       git branch: 'main', url: 'https://github.com/t-node/jgsu-spring-petclinic'
            //}
        //}
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
               
                sh './mvnw clean package'
                 // sh 'false'
                // Run Maven on a Unix agent.
               // sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                //}
                //changed {
                    emailext attachLog: true, 
                    body: 'Please go to ${BUILD_URL} and verify', 
                    compressLog: true, 
                    recipientProviders: [upstreamDevelopers()], 
                    subject: "Job \'${JOB_NAME}\' (${BUILD_NUMBER}) is waiting ${currentBuild.result}", 
                    to: 'vevin1986@gmail.com'
                }
            }
        }
    }
}

