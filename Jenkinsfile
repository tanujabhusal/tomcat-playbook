pipeline {
     agent {
	 
	    lable {
		     lable "Built-in"
			 
			 customWorkspace "/mnt/project/"
		
		}

          }
		  stages {
		  
		  stage ("Clone"){
		    
			steps {
			      sh "rm -rf game-of-life"
				  sh "git clone https://github.com/tanujabhusal/game-of-life.git"
			
			}
		  
		  }
		  
		  stage ("Build") {
		  
		  steps {
		           sh "cd /mnt/project/game-of-life" && mvn install"
				   
				   sh "cd /mnt/project/game-of-life/gameoflife-web/target/ && aws s3 cp gameoflife.war s3://tanuja123"
				   
				   
		  
		  }
		}
		
		stage ('on-slave'){
			 
			 agent { 
			    node {
			       label "ssh-node"
			 
			 customWorkspace "/home/ansible/"
			 }
			 }
			 steps {
			 
			        sh "aws s3 cp s3://tanuja123/gameoflife.war . "
			 
			        sh "git clone https://github.com/tanujabhusal/tomcat-playbook.git "
					
				    sh "ansible-playbook tomcat-assignment.yaml"
			          
                    

			}
			 
			 }
		  
		  
		  }

}
