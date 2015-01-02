# define a makefile variable for the java compiler
# Author: Songyan Hou  Email: sh3348@columbia.edu
JCC = javac

# define a makefile variable for compilation flags
# the -g flag compiles with debugging information
#
JFLAGS = -g

# typing 'make' will invoke the first target entry in the makefile 

default: bfclient.class

bfclient.class: bfclient.java
		$(JCC) $(JFLAGS) bfclient.java



# To start over from scratch, type 'make clean'.  
# Removes all .class files, so that the next make rebuilds them
clean: 
		$(RM) *.class