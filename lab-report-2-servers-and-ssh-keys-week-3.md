# Lab Report 2 Servers and SSH keys

# Part 1
```ChatServer.java```
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
```add-message?s=Hi&user=carloslugo```

<img width="1709" alt="Screenshot 2024-01-29 at 4 21 01 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/74c9c23e-2bac-4b6d-91dc-c066150fd56d">

The handleRequest() method is called
    
```add-message?s=Bye&user=carloslugo```

<img width="1702" alt="Screenshot 2024-01-29 at 4 21 11 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/e838dd32-4661-4921-a058-9fbb83a80d97">









