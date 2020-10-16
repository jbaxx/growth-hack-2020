## Growth Hack 2020 - Big Data
Welcome! Although not strictly Big Data, we'll be learning few tools that make life easier for Data Engineers (and everyone working with data).

## Working in the terminal
The engineers day to day happens in the terminal, may look scary but is hella fun!

We'll use



## Working with text data
### Getting some data
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt
```

Woa, that was actually too fast.
Let's pipe it through the counter to see how many lines we have
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | wc -l
```

Let's remove the punctuation
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | tr -d '[:punct:]' | tr -d '’'
```

I like where we're getting.
Now is time to count the word frequency.
For that let's replace all spaces with new line jump
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | tr -d '[:punct:]' | tr -d '’' | tr '[:space:]' '[\n*]'
```

To make it more interest let's sort it
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | tr -d '[:punct:]' | tr -d '’' | tr '[:space:]' '[\n*]' | sort
```

Now let's count it
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | tr -d '[:punct:]' | tr -d '’' | tr '[:space:]' '[\n*]' | sort | uniq -c
```

Not what we expected, every day problems, let's fix it with syntactic sugar to change the number and word sport, then sort
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | tr -d '[:punct:]' | tr -d '’' | tr '[:space:]' '[\n*]' | sort | uniq -c | awk '{print $2" "$1}'
```

It's looking better, now let's sort it by frequency
If we ommit `-nr` it's sorted lexicographically
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | tr -d '[:punct:]' | tr -d '’' | tr '[:space:]' '[\n*]' | sort | uniq -c | sort -nr
```

And where's the bandersnatch?
```
curl -sN https://www.gutenberg.org/files/12/12-0.txt | tr -d '[:punct:]' | tr -d '’' | tr '[:space:]' '[\n*]' | sort | uniq -c | sort -nr
```

## Working with streaming data
### Getting some data
You should see something like this
![Demo Streaming Data](img/curl_stream.gif)
