pipeline {
    agent any

    tools { nodejs "Newman" }
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/mulesoft-consulting/anypoint-automation-test-postman.git'
            }
        }
        
        stage('Run') {
            environment{
                ANYPOINT_ROOT_ORG_ID = "${params.anypointRootOrganizationId}";
                ANYPOINT_ROOT_ORG_OWNER_ID = "${params.anypointRootOrganizationOwnerId}";
                ANYPOINT_CREDENTIALS = credentials( 'cat-api-test-anypoint-username-password' );
            }

            steps {
                sh 'newman run CAT\\ Test.postman_collection.json --bail --env-var "anypointRootOrganizationId=$ANYPOINT_ROOT_ORG_ID" --env-var "anypointRootOrganizationOwnerId=$ANYPOINT_ROOT_ORG_OWNER_ID" --env-var "anypointUsername=$ANYPOINT_CREDENTIALS_USR" --env-var "anypointPassword=$ANYPOINT_CREDENTIALS_PSW"'
            }
        }
    }
}