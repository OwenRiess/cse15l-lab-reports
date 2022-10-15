***CSE 15l week 1 Lab Report***

**Installing VScode**
- I already had VScode installed before the lab so I didn’t really have to do anything for this step
- To be able to install VScode you have to go to https://code.visualstudio.com/ and choose the version that matches your operating system to install
- When you have VScode installed and opened it should look like the screenshot below

![image](images/VScode.png)


**Remotely Connecting**

- The first thing to verify is that your computer has OpenSSH installed. To verify on Mac you open the menu>System preferences>sharing>remote login. It should look like this

![image2](images/openSSH.png)

- After that step you will have to go https://sdacs.ucsd.edu/~icc/index.php to look up your account and change your password for your cse 15l account
- The next step is to open up the terminal on VScode by Terminal > New Terminal on the menu commands and put in ssh cse15lfa22zz@ieng6.ucsd.edu, but replace the with the last 2 letters in your cse 15l account username. Then click enter.
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

- Then in the terminal you will type out 
scp WhereAmI.java cs15lfa22ql@ieng6.ucsd.edu:~/ in this case WhereAmI.java is the file that I’m moving and ql are the last 2 letters from cse 15l account username. It will then ask for your password.

![image8](images/whereAmIpassword.png)

- After completing the previous step you will then ssh back into the remote desktop and you will then be able to compile and run the file you moved.

![image9](images/FileCopy.png)

**Setting An SSH Key**

 - The first step is to run the ssh -keygen command on your computer then after that you will type out /Users/owenriess/.ssh/id_rsa owenriess is the user in this case then it will ask for you to make a passphrase

 ![image10](/images/settingSSH.png)

 - Then in the terminal you will sign back into the remote desktop cse15lfa22zz@ieng6.ucsd.edu and fill in your password. Once you are signed in you will run the mkdir .ssh command then exit after that.

 ![image11](images/mkdir.png)

 - Once you are logged out you will then type out 
 scp /Users/owenriess/.ssh/id_rsa.pub cs15lfa2ql2@ieng6.ucsd.edu:~/.ssh/authorized_keys in the terminal and put in the password that you created.

![image12](images/password.png)

**Optimizing Remote Running**

- If you want to run a command while logging into the remote server you can write the command you want to do right after the ssh command for example 
ssh cs15lfa22ql@ieng6.ucsd.edu "ls" will list the home directory on the remote server right after logging in 

![image13](images/"LS".png)

- You can use semicolons in order to run multiple commands on the same line in the terminal for example cp WhereAmI.java OtherMain.java; javac Othermain.java; java WhereAmI will compile and run WhereAmI and OtherMain

![image14](images/FileCopy.png)

- A way to write out the commands that you want to type on terminal you can use the up arrow to go through previous commands that you have ran.







**Week 3 Lab Report**
(having weird issue where on vs codes the markdown preview are showing how they are supposed to, but for some reason not showing up properly on page)

**Part 1**
```
class Handler implements URLHandler {

    ArrayList<String> words = new ArrayList<String>();

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("List of words: %s", words);
        } 
        else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("p")) {
                    words.add("pineapple");
                    return String.format("added %s!", parameters[1]);
                }
                else if (parameters[0].equals("a")){
                    words.add("apple");
                    return String.format("added %s!", parameters[1]);
                }
            }
            return "404 Not Found!";
        }
    }
}
```


![image15](images/pineapple2.png)

- Here I called p=pineapple in the query of the url which is supposed to add the string pineapple to my arraylist that I created and return "added pineapple!"

![image16](images/apple2.png)

- In this image I called a=apple in the query of the url which is supposed to add the string apple to my arraylist that I created and return "added apple!"

![image17](images/list.png)

- This image shows what happens when the page is reloaded with nothing in the query. It displays the words that have been added to my arraylist.


**Part 2**

Given code
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

fixed code
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length-1-i];
      arr[arr.length-1-i] = temp;
    }
  }
```
- The faliure inducing input of the given code was that it replacing the numbers one at a time in the array which meant that the numbers that got replaced in the first half were replacing the numbers in the second half of the array.

- The symptom of this was that once the half way mark was reached the numbers in the given reversed array didn't match the array being manipulated by the reverseInPlace method.

- The bug in the code that needed to be fixed was instead of iterating thruogh the whole array only going through half of the array and swaping the numbers in the front and back half around.

 Given Code
```
static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
  ```

fixed code

```
interface StringChecker { boolean checkString(String s); }

class MyStringChecker implements StringChecker {

  public MyStringChecker() {

  }
  public boolean checkString(String s) {
    if (s.equals("word")) {
      return true;
    }
    else {
      return false;
    }
  }

}
class ListExamples {
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }
```
  - The faliure inducing input was that the filter method was trying to pass through a StringChecker object without having anything that implemented the StringChecker interface

  - The symptom was that when writing a test I wasn't able to pass through a StringChecker object.

  - To fix the bug I created a class that implemented StringChecker so I could pass through a valid StringChecker object when writing my test for this method.
















