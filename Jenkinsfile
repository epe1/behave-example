pipeline {
    agent any
    stages {
        stage('Stage 1') {
            steps {
                withPythonEnv('python3') {
                    sh 'pip install -r requirements.txt'
                    sh 'behave -f json -o behave-ouput.json'
                    sh 'ls -la'
                    sh 'python -m behave2cucumber -i behave-ouput.json -o cucumber-report.json'
                }
            }
        }
    }
    post {
    always {
        cucumber buildStatus: 'UNSTABLE',
                failedFeaturesNumber: 1,
                failedScenariosNumber: 1,
                skippedStepsNumber: 1,
                failedStepsNumber: 1,
                fileIncludePattern: '**/*cucumber-report.json',
                sortingMethod: 'ALPHABETICAL',
                trendsLimit: 100
    }
}
}