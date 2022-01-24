node {
        
    def  IMAGE_NAME = 'andylee1973/swift-messaging'    
    def  GIT_TOKEN_ID = 'fstop-andy-lee-github-token'
    def  GIT_USER_MAIL = 'andy_lee@fstop.com.tw'
    def  GIT_USER_NAME = 'fstop-andy-lee'
    def  GIT_REPO = 'swift-messaging-manifest'
    def  DEPLOY_FILE = 'swift-messaging-service-deployment.yaml'
    
    def  GIT_HOST = 'github.com'
    def  GIT_BRANCH = 'master'    
    
    stage('Clone repository') {
        checkout scm
    }

    stage('Update Manifest') {
      script {
        catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
          withCredentials([usernamePassword(credentialsId: GIT_TOKEN_ID, passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
            sh """
                 git config user.email ${GIT_USER_MAIL}
                 git config user.name ${GIT_USER_NAME}
                 sed -i 's+${IMAGE_NAME}.*+${IMAGE_NAME}:${DOCKERTAG}+g' ${DEPLOY_FILE}
                 cat ${DEPLOY_FILE}
                 git add .
                 git commit -m 'Done by Jenkins Job: ${DOCKERTAG}'
                 git push https://${GIT_USERNAME}:${GIT_PASSWORD}@${GIT_HOST}/${GIT_USERNAME}/${GIT_REPO}.git HEAD:${GIT_BRANCH}
               """
          }
        }
      }
    }
}
