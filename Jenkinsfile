
#!groovy

@Library{'jenkinslib'}

def tools = new arg.devops.tools()

String workspace = "/data/www/.jenkins/workspace"

//Pipeline
pipeline{

	agent {
		node {	label "master"	// 运行代码的节点或者标签
			customWorkspace "${workspace}" // 指顶运行工作目录
		
		}
	}
	
	options {
		timestamps() //日志会有时间
		skipDefaultCheckout()
		disableConcurrentBuilds() // 禁止并行
		timeout(time: 1, unit: 'HOURS') // 流水线超时设置 1h
	}

	stages {
		//下载代码
		stage("GetCode"){
			steps{
				timeout(time:5, unit:"MINUTES"){  // 步骤超时时间
					script{ // 填写运行代码
						println('获取代码')
					}
				}
			}
		}

		//构建
		stage("Build"){
			steps{
				timeout(time:20, unit:"MINUTES"){
					script{
						print("代码扫描")
					}
				}
			}
		}

		//代码扫描
		stage("CodeScan"){
			steps{
				timeout(time:30, unit:"MINUTES"){
					script{
						print("代码扫描")
					}
				}
			}
		}

	}


	//构建后操作
	post{
		always{
			script{
				println("alwasy")
			}
		}

		success{
			script{
				currentBuild.description += "\n 构建成功"
			}
		}

		failure {
			script{
				currentBuild.description += "\n 构建失败"
			}
		}

		aborted {
			script{
				currentBuild.description += "\n 构建取消"
			}
		}
	}

}
