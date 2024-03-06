import groovy.json.JsonOutput

def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]

def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}


pipeline {
    //The agent section specifies where the entire Pipeline, or a specific stage, 
    //will execute in the Jenkins environment depending on where the agent section is placed.
    agent any
    
    //The environment directive specifies a sequence of key-value pairs which will be defined
    //as environment variables for all steps, or stage-specific steps, depending on where the environment directive is located within the Pipeline.
    environment {
        BUILD_USER = ''
    }
    
    //The parameters directive provides a list of parameters that a user should provide when triggering the Pipeline.
    //The values for these user-specified parameters are made available to Pipeline steps via the params object, see
    //the Parameters, Declarative Pipeline for its specific usage.
    parameters {
        string(name: 'SPEC', defaultValue: 'cypress/e2e/1-getting-started/**', description: 'cypress examples')
        choice(name: 'BROWSER', choices: ['chrome', 'edge', 'firefox'], description: 'Pick the web browser you want to use to run your scripts')
    }

    //The options directive allows configuring Pipeline-specific options from within the Pipeline itself.
    //Pipeline provides a number of these options, such as buildDiscarder, but they may also be provided by
    //plugins, such as timestamps. Ex: retry on failure
    options {
        ansiColor('xterm')
    }    

    //The stage directive goes in the stages section and should contain a steps section, an optional agent section, 
    //or other stage-specific directives. Practically speaking, all of the real work done by a Pipeline will be wrapped
    //in one or more stage directives.
    stages {
        
        stage('Build'){
            //The steps section defines a series of one or more steps to be executed in a given stage directive.
            steps {
                echo "Building the application"
            }
        }
        
        stage('Testing') {
            steps {
                bat "npm i"
                bat "npx cypress run --browser ${BROWSER} --spec ${SPEC}"
            }
        }
    }

    post {
        always {
            echo "Test suite completed"
        }
    }
}
