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
                messages.add(message);
                return String.join("\n", chatMessage);
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

1. The ```handleRequest()``` method is called. The revelant argument in this screenshot is ```/add-message?s=Hi&user=carloslugo```.
The relevant fields are in the method, user and message. These fields are empty before the method is ran, but when ran with said argurment. When the method is the the user field value becomes ```"carloslugo"``` and the message value becomes ```"Hi"```. These values are changed due to the argument. These values are then stored in two lists that are changed each time an argument is input. 
    
http://localhost:4004/add-message?s=Bye&user=carloslugo

<img width="598" alt="cse-15L-lab-report-2-screenshot-2" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/580cf6b1-d7c3-4eb9-81d3-31fef9007e5e">

2. The ```handleRequest()``` method is called. The revelant argument in this screenshot is ```/add-message?s=Hi&user=carloslugo```.
The relevant fields are the same, user and message. These fields are set to the previous user and message before the method was called again. When the method is called with this argument, the the user field value becomes ```"carloslugo"``` and the message value becomes ```"Bye"```. These values are changed due to the argument. These values are then stored int the lists as well and displayed as a chat message. 

## Part 2
**```ls``` into absolute path of private key**

<img width="495" alt="Screenshot 2024-01-30 at 7 01 55 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/efb5cb4a-0f1c-4a73-bfee-5c294ac291ac">

**```ls``` into absolute path of public key**

<img width="516" alt="Screenshot 2024-01-30 at 7 00 00 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/21cdc94c-c5ca-4914-bb5a-07c5679159c8">

**log into ieng6 account without password**

<img width="579" alt="Screenshot 2024-01-30 at 7 01 16 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/c084b721-510c-4a2c-adfe-9966c81b55a5">











