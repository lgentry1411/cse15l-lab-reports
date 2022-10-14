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

Here is screenshot 3

![Image](/lab-2-images/55.png)

Here is how we search the database with a string. The HandleRequst method is called again, except now the if statement that looks for the path /search
fires. After it does, it again splits the query at the equal sign. Then, it loops through the arraylist strings and checks to see if each string contains
the string we passed into the search. If it does, then that string is added to another arraylist searched. After the loop concludes, the searched arraylist is outputted to the screen.

In this case, we searched for strings with the substring a, so it outputted apple and banana.
    
    
# PART 2
    
## Bug 1
    

In reversedInPlace() in ArrayExamples, there is a bug. 

Failure inducing input:
	
    @Test 
	public void testReverseInPlaceLong() {
        int[] input1 = { 3, 4, 5 };
        ArrayExamples.reverseInPlace(input1);
        assertArrayEquals(new int[]{ 5, 4, 3 }, input1);
	}

This test breaks the code because input1 ends up being equal to [5, 4, 5].
	
Here is the fixed code:
	
    static void reverseInPlace(int[] arr) {
		for(int i = 0; i < arr.length/2; i += 1) {
			int temp = arr[i];
			arr[i] = arr[arr.length - i - 1];
			arr[arr.length - i - 1] = temp;
		}
	}
										
This bug causes the symptom because after placing the replacing the element in the first slot with the element in the last slot, that element that was in the first slot no longer exists. So, when you get to the second half of the array and try to replace the element in the last slot with the element in the first slot, that element in the first slot was already replaced, so the array just ends up being a mirror of the back half of the array.
										
										
## Bug 2
    

In filter() in ListExamples, there is a bug. 

Failure inducing input:
	
    @Test 
	public void testFilter() {
        ArrayList<String> input1 = new ArrayList<>();
        input1.add("apple");
        input1.add("banana");
        input1.add("coconut");
        StringChecker sc = new StringChecker(){ 
            public boolean checkString(String s) {
                return s.length() < 7;
            }
        };
        ListExamples.filter(input1, sc);
        ArrayList<String> output = new ArrayList<>();
        output.add("apple");
        output.add("banana");
        assertArrayEquals(output.toArray(),  ListExamples.filter(input1, sc).toArray());
	}

This test breaks the code because ListExamples.filter(input1, sc).toArray() ends up being equal to [banana, apple] when it should be [apple, banana].
	
Here is the fixed code:
	
	static List<String> filter(List<String> list, StringChecker sc) {
		List<String> result = new ArrayList<>();
		for(String s: list) {
			if(sc.checkString(s)) {
				result.add(s);
			}
		}
		return result;
	}
										
This bug causes the symptom because when adding s to result, the line was first result.add(0, s). This would add elements to the beginning of result, so the list would be backwards. 
										
										
									
