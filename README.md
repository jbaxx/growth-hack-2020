# Growth Hack 2020 - Big Data
## Building ETL Data Pipelines in 5 mins
Perform an ETL: Extract, Transform, Load/Presentation

## Objectives
1. Build a pipeline to extract the word frequency from an unstructured dataset
1. Simulate the implementation decisions Data Engineers face on large scale systems in a short exercise

## Table of Contents
### Part I. Opening a terminal
Get an online discardable workspace
### Part II. Unix pipes
Get a brief into on using Unix pipes, the equivalent for Big Data processing
### Part III. Creating the pipeline
Build the actual ETL for the word count aplication

## Part I. Opening a terminal
Open an online shell using this link:  
#### [https://repl.it/languages/bash](https://repl.it/languages/bash)

### Getting to know the terminal
You will see a prompt like this
```
>
```
Type a command and hit <kbd>Enter</kbd> to execute it.

### Copy and Paste: you can copy and then paste the commands in the terminal using <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>v</kbd>

This one to show all the content of the current folder
```
ls -als
```
This one to print a message
```
echo Hola!
```

## Part II. Unix Pipes
Unix pipes are are mechanisms to transform and communicate data between processes, similar to what Data Engineers do in the Cloud systems.  
The pipe is called using the `|` symbol.

### Your first pipe
Let's print a message like we did before, and then pipe it to another process
1. Echo the message
2. Pass it to a pipe `|`
3. Let the pipe send it to `tr` which will transform it into uppercase
```
echo Hola! | tr a-z A-Z
```
Congratulations! You're ready to get some serious action!

## Part III. Creating the pipeline
### Step 1. Getting some data
Let's get a copy of *Alice Through the Looking-Glass by Lewis Carroll*
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt > alice.txt && cat alice.txt
```

### Step 2. Counting lines
Woa, too fast.
Print it (using `cat`) and pipe it to `wc` (the line counter) to see how many lines we have in total
```
cat alice.txt | wc -l
```

### Start the tweaking - Understanding word frequency
Let's calculate how many times each word appears in the text, for that we'll need to do some processing before

### Step 3. Remove punctuation
Delete punctuation by using the transformer: `tr -d`
```
cat alice.txt | tr -d '[:punct:]’‘'
```

### Step 4. Separating words in lines   
To get the word frequency
1. Put each word in a line by replacing a space (`[:space:]`) with a line jump (`[\n*]`)
2. Count the number of lines
```
cat alice.txt | tr -d '[:punct:]’‘' | tr '[:space:]' '[\n*]'
```

### Step 5. Sorting words
Sort it
```
cat alice.txt | tr -d '[:punct:]’‘' | tr '[:space:]' '[\n*]' | sort
```

### Step 6. Count the sorted words
Now let's count it
```
cat alice.txt | tr -d '[:punct:]’‘' | tr '[:space:]' '[\n*]' | sort | uniq -c
```

### Step 7. Doing a better sort to better count
Not what we expected, every day problems.   
Let's fix it with some syntactic sugar.  
Swap the number and word spot using our friend `awk`, then sort.  
```
cat alice.txt | tr -d '[:punct:]’‘' | tr '[:space:]' '[\n*]' | sort | uniq -c | awk '{print $2" "$1}'
```

### Step 8. Getting the top 20 words
It's looking better, now let's sort it by frequency and get the top 20 only
If we ommit `-nr` it's sorted lexicographically
```
cat alice.txt | tr -d '[:punct:]’‘' | tr '[:space:]' '[\n*]' | sort | uniq -c | sort -nr | head -n 20
```

### Step 9. Finding a word
And where's the bandersnatch?
```
cat alice.txt | tr -d '[:punct:]’‘' | tr '[:space:]' '[\n*]' | sort | uniq -c | sort -nr
```

## Working with streaming data
### Getting some data
You should see something like this
![Demo Streaming Data](img/curl_stream.gif)
