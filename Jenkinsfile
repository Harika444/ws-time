node
  {                   
    stage ('Workspace Cleanup') {
      cleanWs()                             
    }
    stage('Code Checkout')
    {
        git url: 'https://github.com/Harika444/ws-time.git'
    }     
    stage('Build'){       
            sh label: '', script: '''
	    sed -i "s/VERSION/0.0.$BUILD_NUMBER/g" package.json
            auth_token=`aws codeartifact get-authorization-token --domain daxeos --query authorizationToken --output text --duration-seconds 900 --region us-west-2`
            docker build -t daxeos_pkg --build-arg TOKEN=$auth_token .
	          docker rmi daxeos_pkg
            '''
            echo "Build Succcessful"                   
    }
  }
