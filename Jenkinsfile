pipeline{
    agent any
    tools {
        maven "MAVEN"
        jdk "OracleJDK8"
    }
    
    environment {
        SNAP_REPO = 'devops-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = '01672602887.ngtm'
        RELEASE_REPO = 'devops-release'
        CENTRAL_REPO = 'devops-maven-central'
        NEXUS_GRP_REPO = 'devops-maven-groups'
        NEXUSIP = '172.31.8.97'
        NEXUSPORT = '8081'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps{
                sh 'mvn -s settings.xml -DskipTests install'
            }

            post {
                success {
                    echo "Now archiving"
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Test'){
            steps{
                sh 'mvn -s settings.xml test'
            }
        }

        stage('Checkstyle Analysis'){
            steps{
                sh 'mvn -s settings.xml checkstyle:checkstyle'
            }
        }
    }
}