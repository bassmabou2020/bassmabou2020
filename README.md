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

            // Perform login
            boolean authenticated = false;
            do {
                // Request login method
                out.println("login");
                String loginMethod = in.readLine();
                System.out.println("Login method received from client: " + loginMethod);

                // Perform login based on the selected method
                if (loginMethod.equals("password")) {
                    authenticated = performPasswordLogin(in, out);
                } else if (loginMethod.equals("fingerprint")) {
                    authenticated = performFingerprintLogin(in, out);
                } else if (loginMethod.equals("phone")) {
                    authenticated = performPhoneLogin(in, out);
                }

                // Send authentication result to the client
                out.println(authenticated);
            } while (!authenticated);

            // Once authenticated, proceed with communication
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

    private static boolean performPasswordLogin(BufferedReader in, PrintWriter out) throws IOException {
        // Request username and password from the client
        out.println("username");
        String username = in.readLine();
        out.println("password");
        String password = in.readLine();

        // Perform authentication based on the username and password
        // Replace this with your actual authentication logic
        return username.equals("admin") && password.equals("123456");
    }

    private static boolean performFingerprintLogin(BufferedReader in, PrintWriter out) throws IOException {
        // Request fingerprint data from the client
        out.println("fingerprint");
        String fingerprintData = in.readLine();

        // Perform authentication based on the fingerprint data
        // Replace this with your actual fingerprint authentication logic
        // Compare fingerprintData with the stored fingerprint data
        return fingerprintData.equals("stored_fingerprint_data");
    }

    private static boolean performPhoneLogin(BufferedReader in, PrintWriter out) throws IOException {
        // Request phone number from the client
        out.println("phone");
        String phoneNumber = in.readLine();

        // Perform authentication based on the phone number
        // Replace this with your actual phone number authentication logic
        // Compare phoneNumber with the stored phone number
        return phoneNumber.equals("1234567890");
    }

    private static void connectToServer() {
        try {
            Socket socket = new Socket("localhost", PORT);
            System.out.println("Connected to server.");

            // Create input/output streams for communication with the server
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            // Request login method from the server
            String loginMethod = in.readLine();
            System.out.println("Login method received from server: " + loginMethod);

            // Perform login based on the selected method
            boolean authenticated = false;
            if (loginMethod.equals("password")) {
                authenticated = performPasswordLogin(in, out);
            } else if (loginMethod.equals("fingerprint")) {
                authenticated = performFingerprintLogin(in, out);
            } else if (loginMethod.equals("phone")) {
                authenticated = performPhoneLogin(in, out);
            }

            // Send authentication result to the server
            out.println(authenticated);

            // Proceed with communication if authenticated
            if (authenticated) {
                // Read messages from the console and send them to the server
                BufferedReader consoleIn = new BufferedReader(new InputStreamReader(System.in));
                String message;
                do {
                    message = consoleI apologize for the incomplete response. Here's the complete code that includes login by password, fingerprint, and phone number:

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

            // Perform login
            boolean authenticated = false;
            do {
                // Request login method
                out.println("login");
                String loginMethod = in.readLine();
                System.out.println("Login method received from client: " + loginMethod);

                // Perform login based on the selected method
                if (loginMethod.equals("password")) {
                    authenticated = performPasswordLogin(in, out);
                } else if (loginMethod.equals("fingerprint")) {
                    authenticated = performFingerprintLogin(in, out);
                } else if (loginMethod.equals("phone")) {
                    authenticated = performPhoneLogin(in, out);
                }

                // Send authentication result to the client
                out.println(authenticated);
            } while (!authenticated);

            // Once authenticated, proceed with communication
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

    private static boolean performPasswordLogin(BufferedReader in, PrintWriter out) throws IOException {
        // Request username and password from the client
        out.println("username");
        String username = in.readLine();
        out.println("password");
        String password = in.readLine();

        // Perform authentication based on the username and password
        // Replace this with your actual authentication logic
        return username.equals("admin") && password.equals("123456");
    }

    private static boolean performFingerprintLogin(BufferedReader in, PrintWriter out) throws IOException {
        // Request fingerprint data from the client
        out.println("fingerprint");
        String fingerprintData = in.readLine();

        // Perform authentication based on the fingerprint data
        // Replace this with your actual fingerprint authentication logic
        // Compare fingerprintData with the stored fingerprint data
        return fingerprintData.equals("stored_fingerprint_data");
    }

    private static boolean performPhoneLogin(BufferedReader in, PrintWriter out) throws IOException {
        // Request phone number from the client
        out.println("phone");
        String phoneNumber = in.readLine();

        // Perform authentication based on the phone number
        // Replace this with your actual phone number authentication logic
        // Compare phoneNumber with the stored phone number
        return phoneNumber.equals("1234567890");
    }

    private static void connectToServer() {
        try {
            Socket socket = new Socket("localhost", PORT);
            System.out.println("Connected to server.");

            // Create input/output streams for communication with the server
            BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()));
            PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

            // Request login method from the server
            String loginMethod = in.readLine();
            System.out.println("Login method received from server: " + loginMethod);

            // Perform login based on the selected method
            boolean authenticated = false;
            if (loginMethod.equals("password")) {
                authenticated = performPasswordLogin(in, out);
            } else if (loginMethod.equals("fingerprint")) {
                authenticated = performFingerprintLogin(in, out);
            } else if (loginMethod.equals("phone")) {
                authenticated = performPhoneLogin(in, out);
            }

            // Send authentication result to the server
            out.println(authenticated);

            // Proceed with communication if authenticated
            if (authenticated) {
                // Read messages from the console and send them to the server
                BufferedReader consoleIn = new BufferedReader(new InputStreamReader(System.in));
                String message;
                do {
                    message = consoleIn;
}
}
}
