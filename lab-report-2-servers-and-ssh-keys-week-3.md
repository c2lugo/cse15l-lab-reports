# Lab Report 2 Servers and SSH keys

## Part 1
**```ChatServer.java```**
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;


class Handler implements URLHandler {
    private ArrayList<String> messages = new ArrayList<>();
    private ArrayList<String> users = new ArrayList<>();

    public String handleRequest(URI url) {
        if (url.getPath().contains("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String user = "";
            String message = "";

            for (String param : parameters) {
                String[] keyValue = param.split("=");
                if (keyValue.length == 2) {
                    if (keyValue[0].equals("s")) {
                        message = keyValue[1];
                    } else if (keyValue[0].equals("user")) {
                        user = keyValue[1];
                    }
                }
            }

            if (!user.isEmpty() && !message.isEmpty()) {
                String chatMessage = user + ": " + message;
                users.add(user);
                messages.add(chatMessage);
                return String.join("\n", messages);
            }
        }

        return "404 Not Found!";
    }
}


class ChatServer {
    
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

http://localhost:4004/add-message?s=Hi&user=carloslugo

<img width="600" alt="cse-15L-lab-report-2-screenshot1-" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/89d5acc3-de03-4dbd-8589-dbd8d49e5bef">

**Methods called** 

The ```handleRequest()``` method is called
    
http://localhost:4004/add-message?s=Bye&user=carloslugo

<img width="598" alt="cse-15L-lab-report-2-screenshot-2" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/580cf6b1-d7c3-4eb9-81d3-31fef9007e5e">












