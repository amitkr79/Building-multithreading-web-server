# Java Socket Server Implementations

This repository demonstrates **three variations of a simple TCP server in Java**, each highlighting different concurrency models for handling multiple clients:

1. **Multithreaded Server (per-client Thread)**
2. **Thread Pool Server (using ExecutorService)**
3. **Single-threaded Server (sequential handling)**

---

## 🔧 Requirements

- Java 8 or above
- Basic understanding of Java networking (`java.net.Socket`, `java.net.ServerSocket`)

---

## 📁 Project Structure

Server.java // One of the 3 server implementations at a time
Client.java // Simple client to test the servers

---

## 🚀 How to Run

### 1. Compile the Java files

```bash
javac Server.java Client.java
2. Run the Server
```
---
# java Server
Make sure the server is up and listening before running the client.

#3. Run the Client

java Client
You can run the client multiple times (even in a loop) to test concurrency.

# 🧠 Key Concepts Explained
✅ 1. Multithreaded Server (Per Client Thread)

Thread thread = new Thread(() -> server.getConsumer().accept(clientSocket));
thread.start();
A new thread is created for each client connection.

Suitable for a small number of concurrent clients.

Simple to implement but not scalable due to thread overhead.

# ✅ 2. Thread Pool Server (Using ExecutorService)

ExecutorService pool = Executors.newFixedThreadPool(100);
pool.execute(() -> handleClient(clientSocket));
A fixed number of threads are reused to handle multiple clients.

Efficient and scalable under high load.

Prevents creation of too many threads.

Uses ExecutorService to manage thread lifecycle.

# ✅ 3. Single-threaded Server

Socket acceptedConnection = socket.accept();
handleClient(acceptedConnection); // directly
Handles one client at a time, sequentially.

Simple but not suitable for production or multiple clients.

Useful for debugging or learning socket basics.

# 📡 Communication Flow
Client:

Connects to server via TCP socket.

Sends an initial message (optional).

Reads a welcome message from server.

Server:

Accepts client socket.

Sends a message like "Hello from server <IP>".

Closes the connection.

# 🧪 Testing with Multiple Clients
You can simulate load by modifying the client:

```
for (int i = 0; i < 100; i++) {
    new Thread(client.getRunnable()).start();
}
```
Try this with:

Multithreaded server (works fine for small N)

Thread pool server (more controlled concurrency)

Single-threaded server (only one handled at a time)

⚠️ Common Issues
Connection Refused: Server not started before client.

SocketTimeoutException: Server times out before a client connects. (Set a higher timeout or remove it)

Too many open files: Too many simultaneous threads/sockets, especially in multithreaded version.

# ✅ Conclusion
This repo shows how Java handles socket communication with varying degrees of concurrency and control. The thread pool model is best for most real-world use cases due to its efficiency and scalability.

## 📬 Author
Created by Amit Kumar

Feel free to fork, modify, and learn!
