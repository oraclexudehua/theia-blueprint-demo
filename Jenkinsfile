def getServerDev(){
    def remote = [:]
    remote.name = "server-192.168.1.21"
    remote.host = "192.168.1.21"
    remote.port = 22
    remote.allowAnyHosts = true
    withCredentials([usernamePassword(credentialsId: '0e083f38-149a-4f33-a47b-75193e5db8b6', passwordVariable: 'password', usernameVariable: 'userName')]) {
        remote.user = "${userName}"
        remote.password = "${password}"
    }
    return remote
}

def getServerProd(){
    def remote = [:]
    remote.name = "server-192.168.1.81"
    remote.host = "192.168.1.81"
    remote.port = 22
    remote.allowAnyHosts = true
    withCredentials([usernamePassword(credentialsId: '4cc513b1-097a-4fb2-9fc5-242fdc1001a3', passwordVariable: 'password', usernameVariable: 'userName')]) {
        remote.user = "${userName}"
        remote.password = "${password}"
    }
    return remote
}



pipeline {
  agent none

  stages {
           stage('clear work'){
                agent any
                steps {
                    sh 'rm -rf build'
                    sh 'rm -rf node_modules/'
                }
            }
//         stage('pull  code'){
//                 agent any
//                 steps {
//                     git branch: 'main', credentialsId: '21583bad-90d7-4324-ba1f-c970e5871736', url: 'git@github.com:mike-haobo/InsightEpilepsy_WEB.git'
//                     echo '拉取仓库代码main成功'
//                 }


//         stage('pull  code'){
//                 agent any
//                 steps {
//                     git branch: 'dev/v1', credentialsId: '21583bad-90d7-4324-ba1f-c970e5871736', url: 'git@github.com:mike-haobo/InsightEpilepsy_WEB.git'
//                     echo '拉取仓库代码成功'
//                 }
//
//         }

        stage('build'){
            agent {
                     docker { image 'node:14.19.0' }
            }
            steps {
                    sh 'npm --registry https://registry.npm.taobao.org info underscore 1'
                    sh 'npm config set unsafe-perm true'
                    sh 'npm i yarn -g'
                    sh 'yarn '
                    echo 'yarn finish'
                    echo 'build finish'
            }
        }

        stage('delopy'){
            agent any
            steps {
                echo 'delopy finish'
                // script
                //     {
                //     def sshServer = getServerDev()
                //     sshPut remote: sshServer, from: 'build', into: '.'
                //     sshCommand remote: sshServer, command: "rm -rf /opt/www_v2"
                //     sshCommand remote: sshServer, command: "mv ./build  /opt/www_v2 "
                //      sshCommand remote: sshServer, command: "ln -s /data/  /opt/www_v2/data"
                // }
        }
    }
  }
}
