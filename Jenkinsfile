pipeline {
    agent any
    options {
        // Stop the build early in case of compile or test failures
        skipStagesAfterUnstable()
    }
    stages {
        stage('Compile') {
            steps {
                // Compile the app and its dependencies
                sh './gradlew clean assemble --no-daemon'
            }
        }
        stage('Unit test') {
            steps {
                // Compile and run the unit tests for the app and its dependencies
                sh './gradlew clean testDebugUnitTest --no-daemon --no-build-cache'

                // Analyse the test results and update the build result as appropriate
                junit '**/TEST-*.xml'
            }
        }
        stage('Build APK') {
            steps {
                // Finish building and packaging the APK
                sh './gradlew assembleDebug'

                // Archive the APKs so that they can be downloaded from Jenkins
                archiveArtifacts '**/*.apk'
            }
        }
    }
}
