// podTemplate(containers: [containerTemplate(name: 'maven', image: 'maven', command: 'sleep', args: 'infinity')]) {
//   node(POD_LABEL) {
//     checkout scm
//     container('maven') {
//       sh 'mvn -B -ntp -Dmaven.test.failure.ignore verify'
//     }
//     junit '**/target/surefire-reports/TEST-*.xml'
//   }
// }

node ('master') {
  checkout scm
  stage('Build') {
    withMaven(maven: 'M3') {
      if (isUnix()) {
        sh 'mvn -Dmaven.test.failure.ignore clean package'
      }
      else {
        bat 'mvn -Dmaven.test.failure.ignore clean package'
      }
    }
  }
  stage ('Results') {
    junit '**/target/surefire-reports/TEST-*.xml'
    archive 'target/*.jar'
  }
}