# Lab Report 5

## Grade.sh block

    CPATH='.:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar'
    rm -rf student-submission
    git clone $1 student-submission
    echo 'Finished cloning'

    cd student-submission
  
    if [[ -f ListExamples.java ]]
    then
      echo 'ListExamples found'
    else
      echo 'ListExamples missing'
      echo "GRADE: 0%"
      exit 1
    fi
  
    cd ..
    cp TestListExamples.java student-submission 
    echo "Moved Test File"

    cd student-submission
    javac -cp $CPATH *.java 2> output-error.txt

    if [[ $? -ne 0 ]]
    then
      echo "Compile Error"
      cat output-error.txt
      echo "GRADE: 0%"
      exit 1
    else 
      echo "Compile Successful"
    fi

    java -cp $CPATH org.junit.runner.JUnitCore TestListExamples
    if [[ $? == 0 ]]
    then
      echo "Passed All Tests"
      echo "GRADE: 100%"
    else
      echo "Failure Detected"
    fi
    


# Screenshot 1
![Image](/lab-report-5-images/1.png)

# Screenshot 2
![Image](/lab-report-5-images/2.png)

# Screenshot 3
![Image](/lab-report-5-images/3.png)


# Trace of grade.sh for Screenshot 2

The outputs of the commands that remove the directory and clone the repository are empty if they are successful.

In the first if statement, -f ListExamples.java is true if the file ListExamples.java exists. In this case, the file 
does exist so we move to the then statement, which echos that the file is found.

the next command, cp TestListExamples.java student-submission, copies the tests into the directory with the file that needs to be tested.
This allows the tests to be run on the file. 

The next command is javac -cp $CPATH *.java 2> output-error.txt.

This command compiles all the files and puts the stderr output into a new file called output-error.txt. In this case,
that file is empty because the files compile successfully. If there were a compile error, it would be copied into that file.

The next if statement, [[ $? -ne 0 ]], checks if the outputerror.txt file is not empty, meaning it did not compile correctly. It did, so we move to
the else statement, which echos "Compile Successful".


java -cp $CPATH org.junit.runner.JUnitCore TestListExamples is the last command, which runs the tests in the tester file. 

The next if statement, [[ $? == 0 ]], checks if the output of that command is 0. It is 0 if all the tests pass. Since all the tests pass on this 
correct implementation, it echos "Passed All Tests" and "GRADE: 100%".

