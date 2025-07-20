# Chat-Application

This project contains two distinct, but similar, client-server chat applications implemented in Java. Both use basic socket programming to enable communication between a server and one or more clients via the command line.

Let's break down each set of files and then provide key points for your resume.

Project 1: Simple One-to-One Chat (Client.java and Server.java)
This is a basic chat application where one Server instance communicates with one Client instance.

1. Server.java

Purpose: Listens for a single client connection and facilitates a one-to-one chat.

Core Components:

ServerSocket server: Used to listen for incoming client connections on a specified port (7777).

Socket socket: Once a client connects, this Socket object represents the established connection with that client.

BufferedReader br: Reads messages coming from the client.

PrintWriter out: Sends messages to the client.

Constructor (Server()):

Initializes ServerSocket on port 7777.

server.accept(): This is a blocking call that waits until a client connects.

Initializes BufferedReader and PrintWriter using the socket's input and output streams.

Calls startReading() and startWriting() to begin concurrent communication.

startReading() Method:

Runs in a separate Thread.

Continuously reads lines from the client (br.readLine()).

If the client sends "EXIT", the server prints a termination message, closes its socket, and stops reading.

Prints messages received from the client.

startWriting() Method:

Runs in a separate Thread.

Continuously reads input from the server's console (System.in).

Sends this input to the client (out.println(), out.flush()).

If the server user types "EXIT", it closes the socket and stops writing.

main Method:

Entry point for the server application.

Creates an instance of Server, starting the whole process.

2. Client.java

Purpose: Connects to the server and allows a user to send and receive messages.

Core Components:

Socket socket: Represents the connection to the server.

BufferedReader br: Reads messages coming from the server.

PrintWriter out: Sends messages to the server.

Constructor (Client()):

Attempts to establish a Socket connection to "127.0.0.1" (localhost) on port 7777.

Initializes BufferedReader and PrintWriter for communication.

Calls startReading() and startWriting() for concurrent operations.

startReading() Method:

Runs in a separate Thread.

Continuously reads messages from the server.

If the server sends "EXIT", the client prints a termination message, closes its socket, and stops reading.

Prints messages received from the server.

startWriting() Method:

Runs in a separate Thread.

Continuously reads input from the client's console (System.in).

Sends this input to the server.

If the client user types "EXIT", it closes the socket and stops writing.

main Method:

Entry point for the client application.

Creates an instance of Client, initiating the connection and chat.

Key Features of Project 1:

One-to-One Communication: Designed for a single client to connect to a single server.

Concurrent I/O: Uses separate threads for reading and writing on both client and server sides, allowing simultaneous sending and receiving of messages.

Console-Based: All interaction is through the command line.

Simple Termination: Both client and server can terminate the chat by typing "EXIT".

Project 2: Multi-Client Chat (mclient.java and mserver.java)
This project demonstrates a server capable of handling multiple client connections concurrently.

1. mserver.java

Purpose: A multi-threaded server that can accept and manage connections from multiple clients simultaneously.

Core Components:

ServerSocket ss2: Listens for incoming client connections on port 9999.

main Method:

Initializes ServerSocket on port 9999.

Enters an infinite while(true) loop to continuously accept new client connections.

ss2.accept(): For each new connection, it creates a new Socket (sa).

ServerThread st = new ServerThread(sa); st.start();: This is the key to multi-client support. For every new client connection, a new ServerThread is created and started. Each ServerThread will handle communication with one specific client, allowing the main server loop to continue listening for other clients.

ServerThread Class (Inner Class/Separate Class):

Extends Thread, meaning each instance can run independently.

Constructor (ServerThread(Socket s)): Takes the client's Socket as an argument.

run() Method:

Initializes DataInputStream and PrintWriter for communication with its specific client.

Enters a loop to read messages from its client (is.readLine()).

Echoes the received message back to the client (od.println(line); od.flush();). This makes it an echo server, but it could be modified for broader chat functionality.

If the client sends "QUIT", the thread closes its streams and socket, then terminates.

2. mclient.java

Purpose: A simple client designed to connect to the multi-threaded server.

Core Components:

Socket s1: Represents the connection to the server.

DataInputStream br: Reads user input from the console.

DataInputStream is: Reads messages from the server.

PrintWriter os: Sends messages to the server.

main Method:

Attempts to connect to "localhost" on port 9999.

Initializes input/output streams.

Enters a loop where it reads a line from the console (br.readLine()), sends it to the server (os.println(), os.flush()), and then reads and prints the server's response (is.readLine()).

The loop continues until the client types "QUIT".

Closes all streams and the socket upon exiting.

Key Features of Project 2:

Multi-Client Support: The server can handle multiple concurrent client connections by dedicating a new thread to each client.

Echo Server (Basic Functionality): The server's primary function is to echo back whatever the client sends. This can be extended to a broadcast chat or private messaging.

Thread-per-Client Model: A common design pattern for concurrent servers.

Console-Based: All interaction is via the command line.

Termination: Clients can terminate their connection by typing "QUIT".

Overall Project Concepts and Technologies:
Socket Programming (Java.net): Fundamental understanding of Socket, ServerSocket, and establishing network connections.

Input/Output Streams (Java.io): Use of BufferedReader, PrintWriter, InputStreamReader, OutputStreamReader, DataInputStream for text-based communication over network sockets and console.

Multithreading (java.lang.Thread, java.lang.Runnable): Essential for concurrent operations (simultaneous reading and writing, handling multiple clients).

Client-Server Architecture: Demonstrates the basic setup of a server listening for connections and clients initiating connections.

Command-Line Interface (CLI): Interaction through standard input/output.

Basic Error Handling: try-catch blocks are used for IOException and general Exception, though some are empty and could be improved.

Key Points:

Developed a multi-threaded client-server chat application in Java, demonstrating foundational understanding of network socket programming.

Implemented concurrent communication using Java Threads, enabling simultaneous sending and receiving of messages on both client and server sides.

Designed and built a server capable of handling multiple client connections concurrently, utilizing a "thread-per-client" model for scalable communication.

Gained practical experience with Java I/O streams (BufferedReader, PrintWriter, DataInputStream) for efficient data exchange over network sockets.

Engineered a command-line interface for seamless user interaction and message exchange within the chat environment.

Applied core Java networking concepts to establish reliable connections and manage data flow between distributed applications.

Implemented basic connection management, including client and server-initiated termination protocols.






