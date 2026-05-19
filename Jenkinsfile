pipeline{
	agent {label 'Node1'}
	stages{
		stage('Clone'){
			steps{
				sh ''' 
					cd /home/ec2-user/workspace/JavaDemoJob
					rm -rf java-demo-project
					git clone https://github.com/rohithSN/java-demo-project.git
				'''
			}
		}
		stage('Maven build and copy war to the tomcat'){
			steps{
				sh '''
					cd /home/ec2-user/workspace/JavaDemoJob/java-demo-project
					mvn clean package
					cd target
					cd /opt/tomcat/tomcat10/webapps/
					rm -rf *.war
					cd /home/ec2-user/workspace/JavaDemoJob/java-demo-project/target
					cp *.war /opt/tomcat/tomcat10/webapps/
				'''
			}
		}
		stage('Restarting the tomcat'){
			steps{
				sh ''' 
					sudo systemctl restart tomcat
				'''
			}
		}
	}
}
