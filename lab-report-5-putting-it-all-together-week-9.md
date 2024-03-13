# Lab Report 5 Putting It All Together
## Part 1 - Debugging Scenario 
> **Anonymous:** "Hey everyone, I'm kinda stuck trying to get my grader up and running. Every time I run the grading script, it prints that there was a compile error. Not entirely sure why this is happening; maybe some classpath hiccups or script logic got a bit funky. Any ideas to help me out? Would really appreciate it! Here is the output: "
> <img width="890" alt="Screenshot 2024-03-12 at 8 05 18 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/e8c358ac-0ee0-4e17-8346-2a3b639ebe05">

> **TA:** "Hi there, it appears there may be an issue with your script. To further investigate, could you kindly execute the cloned Java file along with your test separately? This will help verify if there is an actual compile error in either of the Java files. Please provide an additional screenshot with the output for closer examination. Thank you."

> **Anonymous:** "Yup, they seem to compile and run properly when ran seperately from the script. What do you think the bug is then?"
> <img width="1311" alt="Screenshot 2024-03-12 at 8 21 41 PM" src="https://github.com/c2lugo/cse15l-lab-reports/assets/156368539/b3b1ddf6-808a-4186-97dd-d45d57fbc313">

> **TA:** Let's take a closer look at the grading script. It seems there might be an issue with your conditional statement. In the script, change this line:
> ```bash
> if [[ $? -eq 0 ]]; then
> ```
