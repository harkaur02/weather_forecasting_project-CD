pipeline {
    agent any
    environment {
        DOCKERTAG = "${BUILD_NUMBER}"
        GIT_USER_NAME ="harkaur02"
        GIT_REPO_NAME = "weather_forecasting_project-CD.git"
    }
    stages {
        stage ('Update helm Manifest file') {
            steps {
                script {
                    //catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        withCredentials([usernamePassword(
                            credentialsId: 'git-credentials',
                            usernameVariable: 'GIT_USERNAME',
                            passwordVariable: 'GIT_PASSWORD'
                        )]) {
                            sh """
                                git config user.email "harkaur02@gmail.com"
                                git config user.name "harkaur02"

                                echo "values.yaml file before update"
                                cat values.yaml
                                
                                
                                echo "values.yaml file after update....."
                                cat values.yaml

                                git add values.yaml
                                git commit -m "updated image tag to current $BUILD_NUMBER"

                                git push https://$GIT_USERNAME:$GIT_PASSWORD@github.com/$GIT_USERNAME/$GIT_REPO_NAME HEAD:main
                            """
                        }
                    //}
                }
            }
        }
    }
}
