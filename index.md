# **Lab Report 1**  

*KEVIN WILLIAM PEOPLES*  
*A17465911*

## Part1
Following is the code for a web server called the StringServer.  
```
import java.io.IOException;
import java.net.URI;

class StringHandler implements URLHandler {
    private StringBuilder messageStorage = new StringBuilder();
    private int messageCounter = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String queryString = url.getQuery();
            String[] parts = queryString.split("=");
            if (parts.length == 2 && parts[0].equals("s")) {
                String message = parts[1];
                messageCounter++;
                messageStorage.append(messageCounter).append(". ").append(message).append("\n");
                return messageStorage.toString();
            }
        }
        return "Invalid request. Use /add-message?s=<message>";
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number!");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new StringHandler());
    }
} 


