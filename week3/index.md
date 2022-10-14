# Part 1: Simplest Search Engine

```java
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;
    ArrayList list = new ArrayList();

    public String handleRequest(URI url) 
    {
        if (url.getPath().equals("/")) 
        {
            return String.format("List of string: %s\n", list.toString());
        } 

        else 
        {
            System.out.println("Path: " + url.getPath());

            if (url.getPath().contains("/add"))
            {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) 
                {
                    list.add(parameters[1]);
                    return String.format("String %s has been added!", parameters[1]);
                }
            }

            else if(url.getPath().contains("/search"))
            {
                String[] parameters2 = url.getQuery().split("=");
                if (parameters2[0].equals("s"))
                {
                    String search_query =  parameters2[1].toString();
                    ArrayList<String> tempList = new ArrayList<String>();

                    for (int i = 0; i < list.size(); i++)
                    {
                        if (list.get(i).toString().contains(search_query) ){
                            tempList.add(list.get(i).toString());
                            }
                        }

                        return tempList.toString();
                    }
                }

                return "404 Not Found!";
            }
        }
    }

    class SearchEngine {
        public static void main(String[] args) throws IOException {
            // if(args.length == 0){
            //     System.out.println("Missing port number! Try any number between 1024 to 49151");
            //     return;
            // }

            // int port = Integer.parseInt(args[0]);

            Server.start(8088, new Handler());
            //  Server.start(port, new Handler());
        }
    }
```
