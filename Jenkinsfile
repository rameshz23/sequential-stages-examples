pipeline {
    agent none

    options {
        preserveStashes(buildCount: 5)
    }
    
    stages {
        stage("build and test the project") {
            agent {
                label "our-build-tools-agent"
            }
            stages {
               stage("build") {
                   steps {
                       sh "./build.sh"
                   }
               }
               stage("test") {
                   steps {
                       sh "./test.sh"
                   }
               }
            }
            post {
                success {
                    stash name: "artifacts", includes: "artifacts/**/*"
                }
            }
        }

        stage("deploy the artifacts if a user confirms") {
            input {
                message "Should we deploy the project?"
            }
            agent {
                label "our-deploy-tools-agent"
            }
            steps {
                unstash "artifacts"
                sh "./deploy.sh"
            }
        }
    }
}
