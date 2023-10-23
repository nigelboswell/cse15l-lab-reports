# Part 1:
StringServer.java code:
~~~
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class StringServer {
    private static StringBuilder message = new StringBuilder();

    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);
        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));
        //start the server
        server.start();
        System.out.println("Server Started!");
    }

    static class messageHandler implements URLHandler {
        @Override
        public String handleRequest(URI uri) {
            if ("/add-message".equals(uri.getPath())) {
                String query = uri.getQuery();
                if (query != null && query.startsWith("s=")) {
                    String messageToAdd = query.substring(2); // Get the string after 's='
                    message.append(message.length() > 0 ? "\n" : "").append(message.length() / 2 + 1)
                    .append(". ").append(messageToAdd);
                }
                return message.toString();
            }
            return "Invalid request";
        }
    }

    public static void main(String[] args) throws IOException {
        start(5000, new messageHandler());
    }
}
~~~

Running /add-message?s=<string> examples:
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/664c06da-c30e-416c-b696-37a988dfcc0c)
This is my first call to my my URL, this means it will run all methods included: start(), messageHandler(), and the main method. They took in the string given after the input: /add-message?s= then added the string to the list of strings displayed, which in this case it would be the only one displayed. message gets adapted to include "Hello", this is due to me using the add message command at the end of my url 
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/2ed5244b-db41-4d9c-9cc5-2f12d29a8788)
This being my second call and still using the same add message input to the url meant I used all the same methods as before. One difference when it comes to the code being run is this time the "How are you" added an additional line to the ongoing *message* string. Other than this no other fields were changed, unless you include the url I used this time.

# Part 2:
Finding and using ls on where I kept my key in my personal computer,
~~~
PS C:\Users\icrea> cd .ssh
PS C:\Users\icrea\.ssh> ls


    Directory: C:\Users\icrea\.ssh


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        10/16/2023   4:24 PM           2655 id_rsa
-a----        10/16/2023   4:24 PM            576 id_rsa.pub
-a----        10/16/2023   4:20 PM            239 known_hosts


PS C:\Users\icrea\.ssh> 
~~~
Finding where I stored the keys on the ieng6 computer
~~~
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/db19ca3c-8048-47d0-ac87-c846b7ae15c7)
~~~
Here I am logging into the ieng6 computer with my ssh authorized key I installed on it from lab. As I am doing this a couple of days afterwards I’m not sure why I need to paste in my key. In lab when I first submitted my sh key to it I had other requirements when logging into the computer other than the ssh command. However, I had to paste my key and then my password this time and can’t figure out how to get around this as I’ve tried many times by this point.
~~~
![image](https://github.com/nigelboswell/cse15l-lab-reports/assets/146788276/07a3bd79-172f-4e75-81e8-eaa256363341)
~~~
# Part 3:

I think this past week has been very engaging and I really enjoyed learning how to run pretty much anything from my terminal, I could see how this can develop more into the year.
