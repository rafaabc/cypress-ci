pipeline {
    agent any

    parameters{
        string(name: 'SPEC', defaultValue: "cypress/integration/examples/**", description: "Enter the script path that you want to execute")
        choice(name: 'BROWSER', choices: ['chrome'], description: "Choose the browser which you want to execute")
    }    

    options{
        ansiColor('xterm')
    }

    stages{
        stage('Building'){
            echo "Building the application"
        }
        stage('Testing'){
            steps{
               bat "npm i"
                bat "npx cypress run --browser ${BROWSER} --spec ${SPEC}"
            }
        }   
    }
}
