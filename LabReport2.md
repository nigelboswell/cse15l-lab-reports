# Part 1:
~~~
StringServer.java code:
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



# Part 2:



# Part 3:

I think this past week has been very engaging and I really enjoyed learning how to run pretty much anything from my terminal, I could see how this can develop more into the year.
