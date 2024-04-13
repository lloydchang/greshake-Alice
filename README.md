# Alice
Giving ChatGPT access to a real terminal..?

Browsing: enabled

Using lots of prompt injections to convince ChatGPT that it can actually operate a computer, and using it to perform real-world tasks. Just ask Alice/ChatGPT for what you want to get done, it will generate the commands to do it, and use the feedback from those commands to either execute more (like installing dependencies etc) or finish with a user-facing natural language summary of the action performed. It can use internet queries, manipulate files, explore the system on it's own or anything else possible in a terminal to fulfill the user prompt. It is not very successful at solving and executing tasks which take many steps yet.

I hope this project can enable us to have a conversation about what will happen when these large language models are inevitably adapted to this task (as we have seen from the leaked ChatGPT headers) but are capable enough to perform more complex tasks. Hopefully it's better to start this conversation now, while ChatGPT can't yet order your pizza successfully for you. AI Safety reading list recommendations at the bottom.

**This version does not run out of the box, as OpenAI has not released an API and I'm not publishing a reversed API. If that changes in the future there will be installation & use instructions. If you want to use it already, you have to make it work yourself- which may or may not violate OpenAI ToS.**

## Disclaimer-avalanche

Disclaimer 0: All executed commands and returned content should be checked by the user. 

Disclaimer 1: This will probably not replace you yet. Currently it's more akin to a better `tldr` which can also execute for you.

Disclaimer 2: This is just me frantically experimenting with ChatGPT.

## Example Questions:
- What is the CPU model and GPU?
- Hey, can you check if there is a trash.txt file in the current directory and if there is, delete it? Let me known if it was there or not.
- Hey, I would like you to build me a basic flask hello world application in the subfolder web unattended. Just execute the commands to get it done and give me a report at the end!
- Find files on this computer relating to <topic>
- Firefox is not responding. Can you help me?
- What is the current stock price of Apple? (it usually tries to `curl` relevant information)

## Control loop
At every step, additional text is inserted to force ChatGPT to engage in this format of use (like a BNF-style grammar).

1. User enters a prompt
2. Model provides one or more terminal commands to accomplish prompt, or a natural language response
3. Commands are executed one after the other, you should be able to skip/accept/deny
4. When commands are done executing, status code + stdout/err goes back to the language model
5. ChatGPT can correct for encountered errors (new commands) or provide a natural language summary of the results.


### Aren't you worried this will escape the sandbox?
After a lot of experimentation, I don't think ChatGPT is able to do this. It fails at complex tasks. But we need to think about what happens with the next version... Let this be a reminder, it's inevitable if these models are continued, right? Alignment seems to become more and more important.

## Limitations/Failure Cases:
- ChatGPT confabulates terminal output
- It adds unnecessary explanations that pollute the bash commands
- It only very rarely responds with multiple command plans after another if something fails or information is missing.
- ChatGPT keeps insisting that it doesn't actually have access to a computer. This is sort of reduced with all the magic strings that are injected to convince it that it's possible.

## AI Safety Recommended Reading
- Robert Miles Introduction to AI Safety (https://www.youtube.com/watch?v=pYXy-A4siMw)
- I'll gladly consider more recommendations.

Another example:

![Real-world example](https://raw.githubusercontent.com/greshake/Alice/master/screenshots/img.png)
