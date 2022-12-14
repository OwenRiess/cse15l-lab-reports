***CSE 15l Lab Report***

**Installing VScode**
- I already had VScode installed before the lab so I didn’t really have to do anything for this step
- To be able to install VScode you have to go to https://code.visualstudio.com/ and choose the version that matches your operating system to install
- When you have VScode installed and opened it should look like the screenshot below

![image](images/VScode.png)


**Remotely Connecting**

- The first thing to verify is that your computer has OpenSSH installed. To verify on Mac you open the menu>System preferences>sharing>remote login. It should look like this

![image2](images/openSSH.png)

- After that step you will have to go https://sdacs.ucsd.edu/~icc/index.php to look up your account and change your password for your cse 15l account
- The next step is to open up the terminal on VScode and put in ssh cse15lfa22zz@ieng6.ucsd.edu, but replace the zz that is highlighted with the last 2 letters in your cse 15l account username. Then click enter.
- Then you will type in the new password that you made and it should look like this.

![image3](images/ssh.png)

**Trying Some Commands**

- The first command is the cd command which is used to move between directories
- The ls -lat command is used to list of all the file on the current directory

![image4](images/ls-lat.png)

- The ls -a command lists what is in the current directory

![image5](images/ls-a2.png)

- The exit command is used to exit out of the remote desktop

![image6](images/exit.png)

**Moving Files With scp**

- The first step is to compile and run the code that is in the file you created using the javac and java commands

![image7](images/whereAmI.png)

- The in the terminal you will type out 
scp WhereAmI.java cs15lfa22ql@ieng6.ucsd.edu:~/ in this case WhereAm.java is the file that I’m moving and ql are the last 2 letters from cse 15l account username. It will then ask for your password.

![image8](images/whereAmIpassword.png)

- After completing the previous step you will then ssh back into the remote desktop and you will then be able to compile and run the file you moved.

![image9](images/FileCopy.png)

**Setting An SSH Key**

 - The first step is to run the ssh -keygen command then after that you will type out /Users/owenriess/.ssh/id_rsa owenriess is the user in this case then it will ask for you to make a passphrase

 ![image10](/images/settingSSH.png)

 - Then in the terminal you will sign back into the remote desktop cse15lfa22zz@ieng6.ucsd.edu and fill in your password. Once you are signed in you will run the mkdir .ssh command then exit after that.

 ![image11](images/mkdir.png)

 -Once you are logged out you will then scp type out 
 /Users/owenriess/.ssh/id_rsa.pub cs15lfa2ql2@ieng6.ucsd.edu:~/.ssh/authorized_keys in the terminal and put in the password that you created.(This step didn’t work for me. I went through the whole process twice and both times my password didn’t work. I will go to office hours to try and resolve my issue)

![image12](images/password.png)

**Optimizing Remote Running**

- If you want to run a command while logging into the remote server you can write the command you want to do right after the  ssh command for example 
ssh cs15lfa22ql@ieng6.ucsd.edu "ls" will list the home directory on the remote server right after logging in 

![image13](images/"LS".png)

- You can use semicolons in order to run multiple commands on the same line in the terminal for example cp WhereAmI.java OtherMain.java; javac Othermain.java; java WhereAmI will compile and run WhereAmI and OtherMain

![image14](images/FileCopy.png)

- A way to write out the commands that you want to type on terminal you can use the up arrow to go through previous commands that you have ran.










