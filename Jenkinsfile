pipeline
{
    agent any
    
    tools 
    {
        maven 'Jenkins_Maven'
        git 'Default'
        jdk 'Jenkins_JAVA'
    }
    
    stages
    {
        stage ('FetchRepo')
        {
            steps
            {
                git 'https://github.com/VGupta434/Edureka-project-1.git'
            }
        }
        
        stage ('Compile')
        {
            steps
            {
                echo 'Compiling'
                sh 'mvn compile'
            }
        }
        
        stage ('Code Review')
        {
            steps
            {
                echo 'Reviewing Code'
                sh 'mvn pmd:pmd'
            }
            
            post
            {
                success
                {
                    recordIssues(tools: [pmdParser(pattern: 'target/pmd.xml')])
                }
            }
        }
        
        stage ('Test')
        {
            steps
            {
                echo 'Testing'
                sh 'mvn test'
            }
            
            post
            {
                success
                {
                    jacoco()
                }
            }
        }
        
        stage('package')
        {
            steps
            {
                echo 'packaging'
                sh 'mvn package'
            }
        }
        
        stage('build docker image')
        {
            steps
            {
                sh 'pwd'
                sh 'whoami'
                sh 'cd /var/lib/jenkins/workspace/$JOB_NAME'
                sh 'pwd'
                sh 'cp /var/lib/jenkins/workspace/$JOB_NAME/target/ABCtechnologies-1.0.war /var/lib/jenkins/workspace/$JOB_NAME/ABCtechnologies-1.0.war'
                sh 'docker build -t vivekgupta434/abcapp:$BUILD_NUMBER .'
            }
        }
    }
}
