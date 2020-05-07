# jenkins_test_server_description
<h2>Automating the deployment and working of the test server and main server archittecture using jenkins</h2>

<h3>1. Installing the required software</h3>

  a. Install Jenkins
  
  b. Install Httpd server
  
  c. Install Docker
  
    * Create 2 docker containers (one for deloying testing environment another for deploying main server environment)
    * In this project both containers are created from 'httpd' image using jenkins
    * testing_server(container for testing) is linked to my testing folder for storing testing source code
    * main_server1(container for testing)  is linked to my main folder for storing main source code
    
<h3>2. Steps for setting up the jenkins environment</h3>

  a. I have created a script to automate the startup of docker, jenkins ,httpd and the docker containers
        https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Automating_Script.png
        
     ** do not use the script if you are running your server/jenkins for the first time. Only use this if the containers are already
        created. Basically it is for restarting the server evironments
        
  b. Create folders for fetching testing code and source code
  
     * testing folder name and path ->/test_server_code
     * main folder name and path ->/maint_server_code
     ** It wolud be better to use the exact same name of location of folders if you are exactly replicating my setup because my setup is
        created accroding to that.
        
  c. Github and git<br>
    github link ->https://github.com/prasadpriyesh1/branch_jenkins_test_server_demo.git<br>
    post commit hook file ->
    https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/post-commit
    
     * I have 2 branches - testing ,testing2
     * Branch 'testing' has the main server code
     * Branch 'testing2' has the test server code
     * so to make changes for testing use 'testing2'
     * post-commit hook
        -after commit in 'testing' branch , push code to github and call job2 of jenkins
        -after commit in 'testing2' branch , push code to github and call job1 of jenkins
        
  d. Jenkins
  
     * I have three jobs 
       I. Test_server(for deploying testing environment)
       II. Main_server(for deploying main environment)
       III. Merge_job(after successful build merge 'testing2' branch to 'testing' and push the code to github)
       ** note : you to pull the updated code to your local git repository after running the merge job for making further changes
       
  e. Main_server job -><br> https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job2_Main_server_p1.png
                        https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job2_Main_server_p2.png
                        https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job2_Main_server_p3.png
                        
  f. Test_server job -><br> https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job1_Test_server_p1.png
                        https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job1_Test_server_p2.png
                        
  g. Merge_job job -><br> https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job3_Merge_job_p1.png
                      https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job3_Merge_job_p2.png
                      https://github.com/prasadpriyesh1/jenkins_test_server_description/blob/master/Job3_Merge_job_p3.png
