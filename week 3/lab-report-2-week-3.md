# Week 3 Lab Report

## Part 1 - Search Engine

Code:

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler  {
    ArrayList<String> strs = new ArrayList<String>();

    public String handleRequest(URI url) {

        if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                strs.add(parameters[1]);
                return ("current list: " + strs);
            }

        }

        if (url.getPath().contains("/search")) {

            String[] parameters = url.getQuery().split("=");
            ArrayList<String> foundStrs = new ArrayList<>();
            String currStr;

            if (parameters[0].equals("s")) {
                for (int i = 0; i < strs.size(); i++) {
                    currStr = strs.get(i);
                    if (currStr.contains(parameters[1])) {
                        foundStrs.add(currStr);
                    }
                }
                return ("found strings: " + foundStrs);
            }
        }

        return "404 Not Found";
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
```
### Running the server and using add:

![Image](week3-1.png)

* First, the main method in the SearchEngine class is called, and it starts the server using the argument provided as the port number. It also creates a Handler object.
* In the Handler class, an empty arrayList of Strings called strs is created which will be used to store the words.
* The user enters the server's url into a browser which includes add? and s=pineapple, which tells the program to add that string to the list of words. It does this by calling the handleRequest method from the Handler class, which takes the url (a URI) entered as an argument.
* The handleRequest method checks if the url provided contains "add" or "search" in the query part of it. In this case it contained "add". It then creates an array called parameters, in which the string to be added ("pineapple") is stored at the index 1. So the value at parameters[1] is added to strs.
* At the end of processing strs changes to include the string given in the url.
* It returns the Arraylist strs so that the user can see the current list of words and confirm that the word was added to it. 

### Using add again:

![Image](week3-2.png)

* Again, when the user enters the url into the browser, handleRequest is called from the Handler class, and it takes the url as an argument.
* It checks if the query contains "add" or "search". Since it contained "add", it adds the string "banana" to strs. 
* Before calling the method, strs was [apple, hello, pineapple, apps]. After processing, strs is changed to contain the string given in the url, and becomes [apple, hello, pineapple, apps, banana].

### Searching for words containing a substring:

![Image](week3-3.png)

* handleRequest is called from the Handler class, and it takes the url entered by the user as an argument.
* It checks if the query of the url contains "add" or "search". Since it contains search, it puts the string "app" into parameters[1]. It also creates a new arrayList called foundStrs to store the strings which contain the substring to search for.
* It then iterates through strs, which is currently [apple, hello, pineapple, apps, app, banana]. If strs[i] contains parameters[1], it adds strs[i] to foundStrs.
* Once it is done processing, it returns foundStrs. strs does not change.
