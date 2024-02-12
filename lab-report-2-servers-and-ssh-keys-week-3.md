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
                // Using String.join to concatenate all messages with newline separator
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

## Screenshot 1 (First message)
http://localhost:40066/add-message?s=Hi&user=carloslugo
<img width="1710" alt="Screenshot 2024-02-12 at 1 45 18 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/7c303061-ae4b-4c48-9e48-86e2f2fc5f5b">


1. The ```handleRequest()``` method is called. The relevant argument in this screenshot is ```http://localhost:40066/add-message?s=Hi&user=carloslugo```. The relevant fields in the ```Handler``` class are ```messages``` and ```users``` which are both array lists that store the previous users and previous messages sent. When the method is called with the argument, ```http://localhost:4004/add-message?s=Hi&user=carloslugo```, the values of these fields change and "carloslugo" is added to the ```users``` list and "Hi" is added to the ```messages``` list. The array lists are updated accordingly based on the query parameters.


## Screenshot 2 (Second message)
http://localhost:40066/add-message?s=Bye&user=carloslugo
<img width="1710" alt="Screenshot 2024-02-12 at 1 46 35 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/ac1540aa-1fa6-4ce1-b5ff-f608970dc621">


2. The ```handleRequest()``` method is called. The relevant argument in this screenshot is ```http://localhost:40066/add-message?s=Bye&user=carloslugo```.
The relevant fields are the same, ```users``` and ```messages```. These fields should have a the previous messages and users stored. Then when the method is called again with the argument ```http://localhost:4004/add-message?s=Bye&user=carloslugo```, the relevant fields change again and "carloslugo" is added to the ```users``` field and "Bye" is added to the ```messages``` field.
## Part 2
**```ls``` into absolute path of private key**

<img width="483" alt="Screenshot 2024-02-12 at 1 51 38 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/15386f43-2b3a-4d09-97ae-550f911fd83f">


**```ls``` into absolute path of public key**

<img width="318" alt="Screenshot 2024-02-12 at 1 59 11 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/35e1e4c1-85de-421c-ad48-cfdf31a3d2c2">


**Log into ieng6 account without password**
<img width="876" alt="Screenshot 2024-02-12 at 2 00 47 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/9d62f01f-04e1-4a0e-b73e-fad3ab25434f">


## Part 3
In the past two weeks, I have learned how to connect and run a server. In lab, I was able to learn how to remotely connect into my CSE 15L account and run a server. On this server, I was able to interact by changing the path and have different texts pop up. I also learned many commands that are useful.












