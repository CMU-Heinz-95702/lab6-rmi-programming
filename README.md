
# lab6-rmi-programming

# 95-702 Distributed Systems             RMI Programming

In our video lecture on service design, we mainly focused on web services.
But, you may recall, binary approaches were also discussed. Binary approaches,
the video points out, are typically far faster than web service based solutions
using json or xml messages. If a binary message is passed from one machine
to another, and if the two machines are using the same programming language,
very little translation work needs to be done. This may result in a much faster
distributed system - there is no need to translate text (xml or json) into a binary
format on the receiving end.

Remote Method Invocation (RMI) is similar in nature to Remote Procedure
Calls (RPC's). RMI, as opposed to RPC, is found in the world of object
oriented programming and distributed objects. RPC is associated with
the more traditional procedural programming languages.

In both cases, the application developer is free to focus on the business
application and, to a large extent, is able to ignore all of the details
that are associated with how messages are passed over the network. This
separation of concerns is important.

In lab work, it is OK to work with others. However, in the end, you
must have a working solution running on your own laptop. For credit, show
your TA or your instructor your working solution on your own laptop.

Note: Before working through this lab, make sure all of your firewalls are turned off.
You should turn them back on after class. Also, make sure your java -version
and javac -version produce the same result. If you get a class not found
error, it is probably wise to visit your environment variables and delete
your "classpath" variable.

It is suggested that you do not use an IDE for this lab. You are encouraged to
use a simple text editor and the command line tooling (javac, java, rmiregistry,
and rmic).

# Part 1. An Introductory Java RMI example


The first part of this lab takes you through the steps of deploying a
simple Java RMI application. It is required that you complete this
introductory exercise before attempting part 2.


Note that the use of rmic is now optional. In other words, in the most
recent versions of Java, you do not need to generate the stub file
and copy it to the client. The stub or proxy is available via the
client side lookup on the registry.

This is a very simple Java RMI application that illustrates the use
of interfaces and the RMIC tool. Note that it is designed to work
from the command prompt. If you are working on a Windows PC, you will
need to have the java bin directory in your path variable.

1. Create two directories from a DOS or Unix prompt. Name one directory
'RMILabServer' and the other directory 'RMILabClient'.

2. Within the server directory, save the following three classes:
Calculator.java, CalculatorServant.java, and CalculatorServer.java.

Compile all the code with the command "javac *.*".

Run RMIC on the servant class with the command "rmic -v1.2 CalculatorServant".

Copy the interface Calculator.java and the stub class to the client. The
stub will be called CalculatorServant_Stub.class.

Within the server directory, start the rmiregistry with the command "rmiregistry".
If you want to run the registry in the background, you may use "rmiregistry &" (Unix) or
"start rmiregistry" (Windows).

Run the server with the command "java CalculatorServer".

Note: The rmi registry is providing a naming service. The client provides a
name and the registry returns a remote object reference.

3. In the client directory, enter the program
CalculatorClient.java.

Compile the code on the client and run with the command "java CalculatorClient".
After experimenting with the client and studying the code, begin the next
exercise.

:checkered_flag:**Completion of Part 1 is this lab's checkpoint.**


# Part 2. Java RMI Programming


4. Write a Java RMI service according to the following specification:

    // The class extends UnicastRemoteObject and implements Bumper

    // The server calls rebind on the rmiregistry giving the remote
    // object the name "bumper".

    public boolean bump() throws RemoteException {
      // A call on bump() adds 1 to a BigInteger held by the service.
      // It then returns true on completion.
      // The BigInteger is changed by the call on bump(). That is,
      // 1 is added to the BigInteger and that value persists until
      // another call on bump occurs.
    }

    public BigInteger get() throws RemoteException {
      // a call on get returns the BigInteger held by the service
    }

5. Write a Java RMI client according to the following specification:

    The main routine performs a lookup on the rmi registry for a remote
    object that implements the Bumber interface. The object is called
    "bumper".

    The main routine creates a BigInteger (called ctr) initialized to 0.
    The main routine creates another BigInteger (called n) initialized to 10000.
    The main routine loops until the ctr equals n. Each time through the loop,
    ctr is incremented by 1. Each time through the loop, the remote  method
    bump is called.

    Before the loop in the main routine begins, set a timer like this:
        long start = System.currentTimeMillis();
    When the loop is finished, find the ending time like this:
        long stop = System.currentTimeMillis();

    At the end of the main routine, display the value of the BigInteger held on
    the server by calling the remote method get(). In addition, display the
    number of seconds that it took to call this service 10,000 times.

:checkered_flag:**For full credit, show a TA that you have a working RMI client and server that meets these
specifications.**
