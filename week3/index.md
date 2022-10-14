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
            if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);
        Server.start(port, new Handler());
        }
    }
```

Here is a list of screenshot that I take for each step:

1. Before I add something to the list, it is an empty. For this, I simply pass the link that generate after we compile the file.

![Image](ListBefore.JPG)

2. I add some words to the list. We are going to use add argument to add the phrase after the query to the list.

![Image](Apple.JPG)

![Image](Pineapple.JPG)

![Image](Melon.JPG)

![Image](Watermelon.JPG)

![Image](Wintermelon.JPG)

3. The list after I add elements. Use the main URL to display the list.

![Image](ListAfter.JPG)

4. We are going to use search argument find the element in the query that has the phrase we input.

![Image](Search.JPG)

# Part 2: Find 2 bugs in 2 different files

## First code:

- Before I make a change:

```java
static void reverseInPlace(int[] arr) 
{
    for(int i = 0; i < arr.length; i += 1) 
    {
        arr[i] = arr[arr.length - i - 1];
    }
}
```

- After I make a change:

```java
static void reverseInPlace(int[] arr) 
{
    for(int i = 0; i < arr.length / 2; i += 1) 
    {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
}
```

* Explanation: Here, we can see 
