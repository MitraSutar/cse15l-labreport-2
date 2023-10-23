StringServer Code
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String stringy = "";
    int number = 0;

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format(stringy);} else {
            if (url.getPath().contains("/add-message")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    number = number + 1;
                    stringy = stringy + String.valueOf(number) + ". " + String.valueOf(parameters[1])+"\n";
                    return String.format(stringy);
                }
            }
            return "404 Not Found!";
        }
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
Screenshots of /add-message
