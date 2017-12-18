env.dockerimagename="buildon/buildon:v2"
node {
   stage ('Code Checkout') {
    checkout scm
     echo "Listing the files in the current dir"
       sh """ls -ltr
       pwd
       """
    
  }
   stage ('Code compile') {
    sh """pwd
          cd "${WORKSPACE}"
          mvn org.talend:ci.builder:6.3.1:generate -f pom.xml -Dcommandline.workspace="${WORKSPACE}/OODLE_GIT" -Dcommandline.host=34.200.55.25 -Dcommandline.port=8002 -Dcommandline.user=ankush.deshpande@cognizant.com
          """
    sh 'sleep 10s'
   }
 stage ('Code Build') {
    sh """pwd
          cd "${WORKSPACE}/target/"
          mvn package -f pom.xml -Dcommandline.workspace="${WORKSPACE}/OODLE_GIT" -Dcommandline.host=34.200.55.25 -Dcommandline.port=8002 -Dcommandline.user=ankush.deshpande@cognizant.com -DprojectsTargetDirectory="${WORKSPACE}/OODLE_GIT/target"
          """
    sh 'sleep 10s'
   }
   stage ('Code Deploy') {
    echo "Deploying code"
    sh"""
      mvn deploy –fn –e
    """
   }
}
