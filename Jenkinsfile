pipeline {
    agent any
    tools {
        maven "MAVEN3"
        jdk "OracleJDK11"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'admin123'
        RELEASE_REPO = 'vprofile-release'
        CENTRAL_REPO = 'vpro-mavan-central'
        NEXUSIP = "172.31.43.111"
        NEXUSPORT = '8081'
        NEXUS_GRP_REPO = 'vpro-maven-grp'
        NEXUS_LOGIN = 'nexuslogin'        
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }

            post {
                success {
                    echo "Archiving."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }

        stage('Test'){
            steps {
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
