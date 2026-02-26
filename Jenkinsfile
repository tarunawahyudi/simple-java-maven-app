node {

    docker.image('maven:3.9.9-eclipse-temurin-17').inside {

        try {

            stage('Build') {
                sh 'mvn -B -DskipTests clean package'
            }

            stage('Test') {
                try {
                    sh 'mvn test'
                } finally {
                    junit 'target/surefire-reports/*.xml'
                }
            }

            stage('Deliver') {
                sh './jenkins/scripts/deliver.sh'
            }

        } catch (err) {
            currentBuild.result = 'FAILURE'
            throw err
        }

    }
}
