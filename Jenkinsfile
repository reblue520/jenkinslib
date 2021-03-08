#!groovy

@Library('jenkinslib@main') _

//func from shareibrary
def build = new org.devops.build()
def tools = new org.devops.tools()
def toemail = new org.devops.toemail()


//env
String buildType = "${env.buildType}"
String buildShell = "${env.buildShell}"
String srcUrl = "${env.srcUrl}"
String branchName = "${env.branchName}"

userEmail = "2560350642@qq.com"


//pipeline
pipeline{
    agent { node { label "build"}}
    
    
    stages{

        stage("CheckOut"){
            steps{
                script{
                   
                    
                    println("${branchName}")
                
                    tools.PrintMes("获取代码","green")
                    checkout([$class: 'GitSCM', branches: [[name: "${branchName}"]], 
                                      doGenerateSubmoduleConfigurations: false, 
                                      extensions: [], 
                                      submoduleCfg: [], 
                                      userRemoteConfigs: [[credentialsId: 'gitlab-admin-user', url: "${srcUrl}"]]])

                }
            }
        }
        stage("Build"){
            steps{
                script{
                
                    tools.PrintMes("执行打包","green")
                    build.Build(buildType,buildShell)
                    
                    
                    
                    //展示测试报告
                    publishHTML([allowMissing: false, 
                                 alwaysLinkToLastBuild: false, 
                                 keepAll: false, 
                                 reportDir: 'result/htmlfile', 
                                 reportFiles: 'SummaryReport.html,DetailReport.html', 
                                 reportName: 'InterfaceTestReport', 
                                 reportTitles: ''])
                }
            }
       }
    }
    post {
        always{
            script{
                println("always")
            }
        }
        
        success{
            script{
                println("success")
                toemail.Email("流水线成功",userEmail)
            
            }
        
        }
        failure{
            script{
                println("failure")
                toemail.Email("流水线失败了！",userEmail)
            }
        }
        
        aborted{
            script{
                println("aborted")
                toemail.Email("流水线被取消了！",userEmail)
            }
        
        }
    
    }
    
    
}
