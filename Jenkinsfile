pipeline {
    agent none

    stages {
        stage("build and deploy on Centos and Ubuntu") {
            parallel {
                stage("centos") {
                    agent {
                        label "centos"
                    }
                    stages {
                        stage("build") {
                            steps {
                                sh "./run-build-centos.sh"
                            }
                        }
                        stage("deploy") {
                            when {
                                branch "parallel"
                            }
                            steps {
                                sh "./run-deploy-centos.sh"
                            }
                        }
                    }
                }

                stage("ubuntu") {
                    agent {
                        label "ubuntu"
                    }
                    stages {
                        stage("build") {
                            steps {
                                sh "./run-build-ubuntu.sh"
                            }
                        }
                        stage("deploy") {
                             when {
                                 branch "master"
                             }
                             steps {
                                sh "./run-deploy-ubuntu.sh"
                            }
                        }
                    }
                }
            }
        }
    }
}
