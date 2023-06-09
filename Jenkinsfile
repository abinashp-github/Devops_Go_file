pipeline {
    agent any
    
    stages {
        stage('Checkout my project') {
           steps {
               cleanWs()
               git credentialsId: '58270b45-cf28-459f-abe9-0d262896f67d', url: 'https://github.com/abinashp-github/Devops_Go_file.git'
            }
        }
        
        stage('build') {
            steps {
                sh "npm install express"
            }
        }
        
        stage('test') {
            steps {
                sh "node --test"
            }
        }
        
        stage('Copying artifact to Staging (target VM)') {
            steps {
            sshagent(['target']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.89.161"
                sh "scp /var/lib/jenkins/workspace/newjob/index.js ec2-user@172.31.89.161:/home/ec2-user/"
                }
            }
        }
        stage('Deployment in Staging') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'mytarget', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo yum update -y', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'mytarget', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo yum install nodejs -y', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'mytarget', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo yum install npm -y', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'mytarget', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'npm install express', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'mytarget', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'nohup node index.js &>/dev/null &', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        
        stage('Copying artifact to Production (another VM)') {
            steps {
            sshagent(['newEC2']) {
                sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.94.214"
                sh "scp /var/lib/jenkins/workspace/newjob/index.js ec2-user@172.31.94.214:/home/ec2-user"
              }    
            }
        }
        stage('Deployment in Production') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'newEC2', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo yum update -y', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'newEC2', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo yum install nodejs -y', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'newEC2', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo yum install npm -y', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'newEC2', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'npm install express', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                sshPublisher(publishers: [sshPublisherDesc(configName: 'newEC2', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'nohup node index.js &>/dev/null &', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'main')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
        
    }
}
