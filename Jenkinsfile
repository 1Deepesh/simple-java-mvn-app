1. create a jenkins pipeline job.
2. declarative pipeline
3. where my pipeline should run.
4. tools my pipeline should use.
5. my pipeline will always maintain 10 max builds.
6. checkout the sourcecode from git.
7. build the source code using maven.


pipeline{
    agent any

    option{
        properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '10', numToKeepStr: '2'))])

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
