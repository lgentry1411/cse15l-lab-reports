# Lab Report 1

Here is how to connect to a course-specific account on ieng6! (Mac only)

## Step 1: Install VSCode

Go to the this link: [Link](https://code.visualstudio.com/)

Press Download

Unzip and Open

It should look like this:

![Image](/lab-1-images/1.png)



## Step 2: Remotely Connecting

In VSCode, open a new terminal by pressing terminal > new terminal

Enter this command with your specific ID: 

**ssh cs15lfa22zz@ieng6.ucsd.edu**

Enter your password and you should see this.

![Image](/lab-1-images/2.png)


You are now connected!!





## Step 3: Trying some commands

Now you can try some commands and see what happens.

Try:

**ls**

**cd**

**ls -lat**

**ls -a**

**cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/**

And others

And see what they do.

![Image](/lab-1-images/3.png)



## Step 4: Moving Files with scp

Now let’s move a file from our computer to the remote computer.

First use exit to log out.

Now, create a new java file called WhereAmI.java and copy this code:



  class WhereAmI {

      public static void main(String[] args) {

        System.out.println(System.getProperty("os.name"));

        System.out.println(System.getProperty("user.name"));

        System.out.println(System.getProperty("user.home"));

        System.out.println(System.getProperty("user.dir"));

      }

  }



In the terminal run

**javac WhereAmI.java**

**Java WhereAmI**

Take not of the output, it should look like this:

![Image](/lab-1-images/4.png)

Now let’s copy that file to the remote computer.

Copy this command into the terminal: 

**scp WhereAmI.java cs15lfa22zz@ieng6.ucsd.edu: ~/**

Make sure to change the zz to your id 

Enter your password.

If it worked you will see this:

![Image](/lab-1-images/5.png)


Now reconnect to the computer with 

**ssh cs15lfa22zz@ieng6.ucsd.edu**

Type the command **ls**.

You should notice that the file WhereAmI.java is now there.

![Image](/lab-1-images/6.png)

WhereAmI.class will be there too if you compile it.

Next run that file with 

**javac WhereAmI.java**

**Java WhereAmI**

The output should look like this:

![Image](/lab-1-images/7.png)


## Step 5:

Now let’s set an SSH Key so we don’t have to type in that password every time!

Make sure you exit and then use the command 

**ssh-keygen**

It will ask for a you to enter a file to save the key, just press enter if the line ends with is_rsa

Enter a “passphrase” (a shorter password)

It should output a picture like this:

![Image](/lab-1-images/8.png)

Next, reconnect to the server using 

**ssh cs15lfa22zz@ieng6.ucsd.edu **

And your password

Run the command: **mkdir .ssh**

If it says that the file exists, don’t worry about it and move on.

Exit the remote computer

Run this command to copy the key to the remote computer:

**scp /Users/<your_username>/.ssh/id_rsa.pub**

**cs15lfa22zz@ieng6.ucsd.edu:~/.ssh/authorized_keys**

Make sure to add your username on your Mac and your id.

![Image](/lab-1-images/9.png)

If it works it will look like this.



Now try to connect again with 

**ssh cs15lfa22zz@ieng6.ucsd.edu**

It should now look like this:

![Image](/lab-1-images/10.png)


Enter your passphrase and it should connect!

## Step 6: Optimizing Remote Running!

You can also write extra command lines at the end of an ssh connection line to run it immediately on the server. For example:

**ssh cs15lfa22zz@ieng6.ucsd.edu ls**

It should look like this:

![Image](/lab-1-images/11.png)


You can also run multiple commands with semicolons. For example: 

**cp WhereAmI.java OtherMain.java; javac OtherMain.java; java WhereAmI**


Done!
