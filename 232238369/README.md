### HOW I MADE IT/ CHALLENGES I FACED AND SOLUTIONS

Read the whole assignment.
Started by reading test file, 1-1-simple-send.conf and given test code.
Tried running code the few times to see the print statements
Then I started handling messages and begin with update message type

I created the handle_message function to handle various possible message types
Then I started with update funciton to handle update type messages.

Here I wrote code to create and handle forwarding table and send announcement to neighbors. I tested my code with first config file and moved forward

I created the data function to handle data type messages.
I deconstructed the msg_json and went thorugh the forwarding table to find the right route for the message. If no route is found, it results in sedngin a empty message back to sender otherwise sends message to closest neighbor based on rules

Thoughtout the process, the main issue I was facing was how I was creating and working with forwarding table. Earlier I just had a mapping of network to it's attributes but in part2, I realized that network could be same with different attributes, so I changed my approach
I decided to have a array of possible routes for a network
I managed to fix it by trial and error

Then I created the dump function which uses aggregated table.
The creation of aggregation table was slightly challenging but I managed to do do it with python debugger and trial and error

In tests configs 2-.., I realized some of my conditions to choose the route in data function were wrong.
I ran through each test case in 2 and each of them test for particular condition. So I fixed my if conditions one by one and at the end had the right answer

Test case 3 was easy did not face much issues

Test case 4 were a bit confusing, my router was not able to properly identify relationship of src routes, to solve this I abstracted the code for finding the best route and repurposed it so it could find the closest src and that fixed the relationship issue

Test case 5 was hard to crack, I was confused how to make the ip addresses properly and watched a lot of tutorials to see how ip address and CIDR notation works and how subnet values dictate the host and configurable details of the ip addresses.

I managed to create validation function to see if two addresses match

Test case 6
For test case 6, I made sure the addresses are being grouped properly so they can be easily summarized. I was facing a lot of issues with this test case because there were many ip addresses close to one another. Earlier I was summarizing them individually which made the prefix smaller so I could not summaize the next ip address. The solution I figured out was to group them together first so they can be summarized together and this would calcualte the prefix more accurately

### WHAT I THINK IS GOOD WITH MY APPROACH

- A global function handle_message to handle messages
- defining IP manipulation function outside of main class to use it everywhere without self.
- code abstraction and using helper functions with clear arguemnts and return values
- updating and maintaing routing table after every update and withdraw function call
- grouping the ip addresses so the summarizable ip addresses are together and the prefx calculation is easier

# HOW I TESTED MY CODE

- I used the given config files
- I duplicated and updated few config files to 3 myTest files and updated the test file and added
  runTest("myTest1.conf")
  runTest("myTest2.conf")
  runTest("myTest3.conf")
  to test against my cases

in the test cases, I tested if the router sends no route message if no route could be found in data, checked if the aggregation works after disaggregation with withdraw message and tested how close ip addresses get aggregated
