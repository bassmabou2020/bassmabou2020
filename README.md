```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;

public class CommunicationApp {
    private static final int PORT = 1234;

    public static void main(String[] args) {
        // Start the server
        Thread serverThread = new Thread(() -> startServer());
        serverThread.start();

        // Wait for a few seconds to ensure the server starts first
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        // Connect to the server as a client
        connectToServer();
    }

    private static void startServer() {
        try {
            ServerSocket serverSocket = new ServerSocket(PORT);
            System.out.println("Server started. Waiting for a client...");

            // Wait for a client to connect
            Socket clientSocket = serverSocket.accept();
            System.out.println("Client connected.");

            // Create input/output streams for communication with the client
            BufferedReader in = new BufferedReader(new InputStreamReader(clientSocket.getInputStream()));
            PrintWriter out = new PrintWriter(clientSocket.getOutputStream(), true);

            // Read messages from the client and send responses
            String message;
            do {
                message = in.readLine();
                System.out.println("Received from client: " + message);
                out.println("Server received: " + message);
            } while (!message.equals("bye"));

            // Close the connection
            in.close();
            out.close();
            clientSocket.close();
            serverSocket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void connectToServer() {
        try {
            Socket socket = new Socket("localhost", PORT);
            System.out.println("Connected to server.");

            // Create input/output streams for communication with the server
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            // Read messages from the console and send them to the server
            BufferedReader consoleIn = new BufferedReader(new InputStreamReader(System.in));
            String message;
            do {
                message = consoleIn.readLine();
                out.println(message);
                System.out.println("Server response: " + in.readLine());
            } while (!message.equals("bye"));

            // Close the connection
            in.close();
            out.close();
            socket.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
