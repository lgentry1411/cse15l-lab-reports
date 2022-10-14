# Part 1: Search Engine
## Code:

    import java.io.IOException;
    import java.net.URI;
    import java.util.ArrayList;
    import java.util.Arrays;

    class Handler implements URLHandler {
        // The one bit of state on the server: a number that will be manipulated by
        // various requests.
        ArrayList<String> strings = new ArrayList<String>();
        ArrayList<String> searched = new ArrayList<String>();

        public String handleRequest(URI url) {

            if (url.getPath().equals("/")) {
                return String.format("Search Engine!");

            } else {
                System.out.println("Path: " + url.getPath());
                if (url.getPath().contains("/add")) {
                    String[] parameters = url.getQuery().split("=");
                    if (parameters[0].equals("s")) {
                        strings.add(parameters[1]);
                        return String.format("Added: %s", parameters[1]);
                    }
                }
                if (url.getPath().contains("/search")) {
                    searched.clear();
                    String[] parameters = url.getQuery().split("=");
                    if (parameters[0].equals("s")) {
                        for (int i = 0; i < strings.size(); i++) {
                        if (strings.get(i).contains(parameters[1])) {
                                searched.add(strings.get(i));
                            }
                        }
                        return String.format(Arrays.toString(searched.toArray()));

                    }
                }
                return "404 Not Found!";
            }
        }
    }

    class SearchEngine {
        public static void main(String[] args) throws IOException {
            if(args.length == 0){
                System.out.println("Missing port number! Try any number between 1024 to 49151");
                return;
            }

            int port = Integer.parseInt(args[0]);

            Server.start(port, new Handler());
        }
    }

This is the code for my Search Engine!

Here is screenshot 1:

![Image](/lab-2-images/111.png)

This is the home page of my Search Engine. The Method called is the HandleRequest method and it is checking that the path is just a /. If that is the path, it will simply output Search Engine! to the screen.

Here is screenshot 2:

![Image](/lab-2-images/22.png)

Here is how we add something to the database. Again, the HandleRequest method is called except now it checks that the path is /add. After that if statement
fires, it gets the query and splits it at the equal sign. It then adds the second element, so what was after the equal sign, to an arraylist strings. If the add was succesful, it will output Added: <your string> to the screen.

After this I then add two more items, banana and coconut

Here is screenshot 3:

![Image](/lab-2-images/55.png)

Here is how we search the database with a string. The HandleRequst method is called again, except now the if statement that looks for the path /search
fires. After it does, it again splits the query at the equal sign. Then, it loops through the arraylist strings and checks to see if each string contains
the string we passed into the search. If it does, then that string is added to another arraylist searched. After the loop concludes, the searched arraylist is outputted to the screen.

In this case, we searched for strings with the substring a, so it outputted apple and banana.
 

    
    
    
    





