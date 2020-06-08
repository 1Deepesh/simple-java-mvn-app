pipeline{
    agent any
    tools{
        maven 'M2_HOME'
    }

    options{
        buildDiscarder(logRotator(numToKeepStr: '1', artifactNumToKeepStr: '1'))
    }
    stages{
        stage("Display PATH of Jenkins"){
            steps{
                sh '''
                    echo "This s my declarative pipeline"
                    echo "PATH = $(PATH)" '''
            }
        }
        stage("checkout the sourcecode"){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/jenkins-docs/simple-java-maven-app.git']]])
            }
        }
        stage("building the maven project"){
            steps{
                sh 'mvn clean compile install'
            }
        }
        stage("archiving the artifacts"){
            steps{
                archiveArtifacts '**/**/*.jar'
            }
        }
    }
}
