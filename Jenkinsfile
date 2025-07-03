pipeline{
    agent any
    stages{
        stage('scm'){
            steps{
                checkout scm
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install'
            }
        }
        stage('nexus'){
            steps{
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'onlinebookstore',
                        classifier: '',
                        file: 'target/onlinebookstore-0.0.1-SNAPSHOT.war',
                        type: 'war'
                        ]
                    ],
                        credentialsId: 'nexuscred',
                        groupId: 'onlinebookstore',
                        nexusUrl: '13.201.228.238:8081',
                        nexusVersion: 'nexus3',
                        protocol: 'http',
                        repository: 'maven-snapshots',
                        version: '0.0.1-SNAPSHOT'
            }
        }
        stage('deploy') {
    steps {
        step([$class: 'DeployPublisher',
            adapters: [[$class: 'Tomcat9xAdapter',
                credentialsId: 'tomcatcred',
                url: 'http://3.110.209.60:8080']],
            contextPath: '/',
            war: 'target/onlinebookstore-0.0.1-SNAPSHOT.war'
        ])
    }
}
    }
}






