# Lab Report 5
_Created by: Minh Nhat Duong_

[Part 1 - Demonstrate]()

[Part 2 - Tracing]()

## Part 1: Demonstrate Lab

```C++
# Variables
STU_REPO=student-submission
TEST_FILE=TestListExamples
C_ERR=CompileErr
P_ERR=ProgramErr

CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

GRADE=0
TOTAL=5
PERCENTAGE=0

# Remove all old material to not overwriting
rm -rf $STU_REPO
rm -f *.class

# Start cloning student submission
git clone $1 $STU_REPO
echo ''
echo 'Finished cloning'
echo ''

# Check if it successfully clones the repo
if [ $? -ne 0 ]
then 
	echo '[+0] Repository is not found'
else
	echo '[+1] Successful cloning the repository'
	GRADE=$(( GRADE + 1 ))

	# Access to the repo to check if there is a java file exist
	cd $STU_REPO

	if [ ! -f 'ListExamples.java' ]
	then
		echo '[+0] No file existed!'
	else
		echo '[+1] File exist!'
		GRADE=$(( GRADE + 1 ))
	fi

	# Go back to main repo and copy the test file to student-submission repo
	cd ..
	cp $TEST_FILE.java $STU_REPO/
	cp -r lib $STU_REPO/

	# Go to student-submission repo and run JUNIT
	# We need to check whether there is any error for compiling file and run file
	cd $STU_REPO
	javac -cp $CPATH *.java 2> $C_ERR.txt

	if [ $? -ne 0 ]
	then 
		echo "[+0] Compile failure! Check $C_ERR.txt for more information"
	else
		echo '[+1] Success compiling a file'
		GRADE=$(( GRADE + 1 ))
		java -cp $CPATH org.junit.runner.JUnitCore $TEST_FILE > $P_ERR.txt

		if ( grep -q 'testFilter' $P_ERR.txt )
		then
			echo "[+0] Test Filter failure! Check $P_ERR.txt for more information"
		else
			GRADE=$(( GRADE + 1 ))
			echo '[+1] Test Filter success!'
		fi

		if ( grep -q 'testMerge' $P_ERR.txt )
		then
			echo "[+0] Test Merge failure! Check $P_ERR.txt for more information"
		else
			GRADE=$(( GRADE + 1 ))
			echo '[+1] Test Merge success!'
		fi
	fi
fi

# Display your score
PERCENTAGE=$(( $GRADE * 100 / $TOTAL ))
echo ''
echo "Your grade: $GRADE/$TOTAL points => Percentage: $PERCENTAGE%"

```



## Part 2: Tracing
