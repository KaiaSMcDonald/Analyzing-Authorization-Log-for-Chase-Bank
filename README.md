# Analyzing-Authorization-Log-for-Chase-Bank

Down below will lay out the steps I took to try to create a script that would read through each line of the log file,search for keywords that indicate that suspicious login happened, and write the line that contain these keywords into a new log named "suspicious_activity.log'. 

The 1st step I made was use the command 'curl -L "https://github.com/kura-labs-org/install-sh/blob/main/auth_log_creation.sh"' 
I used this command to get the raw contents of the auth_log_creation.sh file within the repository that it is held in. 
This is the result of running that command: 

![Screenshot 2024-08-05](https://github.com/KaiaSMcDonald/Analyzing-Authorization-Log-for-Chase-Bank/blob/main/Screenshot%202024-08-05%20at%205.54.46%20PM.png) <br>



Following that I created a .sh file named "analyze_authlog.sh" that would include a bash script that would do the things mentioned above. 

The bash script included in "analyze_authlog.sh" is as follows: 


![Screenshot 2024-08-05](https://github.com/KaiaSMcDonald/Analyzing-Authorization-Log-for-Chase-Bank/blob/main/Screenshot%202024-08-05%20at%208.49.03%20PM.png) <br>


- First I defined all the keywords I wanted to be used as a indicator for suspicious activity within the log. <br> <br>
- Then I put the absolute path of the authentication log that I will be analyzing <br> <br>
- Next I defined the destination or where I want the lines that contain those keywords to go <br> <br>
- Following that I used 'while IFS= read -r line" to make sure that the script reads the file line by line <br>
(IFS - prevents trailing whitespace from being trimmed and '-r'- prevents backslash escapes from being interpreted)
without using IFS and '-r' the script will fail to read the file line by line and possibly miss out on suspicious activity <br> 
- Then I check if each line has any suspicious keywords by using 'gre -iq' which specifically looks if the file contains patterns with presenting a output. In this case it will quitely check if each line contains the keywords mentioned above in the script.
- Lastly I included the echo command to notify me that every line that includes these keywords were successful written to the "suspicious_activity.log" <br> <br>


Afterwards I ran the "analyze_authlog.sh" script I created. Unfortunately I received an error stating the file I put for the input doesn't exists

In attempt to fix this issue I ran the command 'curl -o auth_log_creation.sh https://github.com/kura-labs-org/install-sh/blob/main/auth_log_creation.sh.<br>


![Screenshot 2024-08-05](https://github.com/KaiaSMcDonald/Analyzing-Authorization-Log-for-Chase-Bank/blob/main/Screenshot%202024-08-05%20at%206.59.32%20PM.png) <br>


This specific would allow me to download that .sh file within the github repository that it is held in. Unfortunately I continue to get the same error message. <br>


The next attempt I made to resolve the issue was clone the entire repository and and then extract that specific file.<br>
By using the following commands:<br>
'git clone https://github.com/kura-labs-org/install-sh.git '<br>
'cd install-sh'<br>
'cat auth_log_creation.sh'(I used this to look at the content of the script to see if everything is was downloaded successfully)





After running those commands I decided to run the analyze_authlog.sh I created but I received and error stating that no such file exists <br>
I realized that the analyze_authlog.sh doesn't exist in the 'install-sh' repository meaning I have to move it there.

I successfully moved the script I created into the 'install-sh' repository but it seems like somewhere in my script I am unable to access the authorized log I need to analyze. <br>





## Conclusion<br>

I think there is a issue with the path I used for input_log_file in my script. However I am not certain where the specific change needs to be made in the path because I did run a 'ls' command and the files are in the "install-sh" directory.







