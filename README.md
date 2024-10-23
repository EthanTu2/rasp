# RASP 

## Setup
#### Mac or Linux
Run `./setup.sh` . It will create a python3 virtual environment and install the dependencies for RASP. It will also try to install graphviz (the non-python part) and rlwrap on your machine. If these fail, you will still be able to use RASP, however: the interface will not be as nice without `rlwrap`, and drawing s-op computation flows will not be possible without `graphviz`. 
After having set up, you can run `./rasp.sh` to start the RASP read-evaluate-print-loop. 

#### Windows
Follow the instructions given in `windows instructions.txt`

## The REPL
After having set up, if you are in mac/linux, you can run `./rasp.sh` to start the RASP REPL. Otherwise, run `python3 RASP_support/REPL.py`
Use Ctrl+C to quit a partially entered command, and Ctrl+D to exit the REPL.


**Problem 1:**
Write an s-op that contains the indices in reverse order.
For example:
```
> reverse_indices("hello")
[4, 3, 2, 1, 0]
```

**Solution:**
```
>> reverse_indices = length - indices - 1;
     s-op: reverse_indices
         Example: reverse_indices("hello") = [4, 3, 2, 1, 0] (ints)
>> reverse_indices("hello");
         =  [4, 3, 2, 1, 0] (ints)
```

**Problem 2:**
Write a function that "rotates" the input text by the specified number of characters.
For example:
```
> rotate(tokens, 0)("hello")
"hello"
> rotate(tokens, 1)("hello")
"ohell"
> rotate(tokens, 2)("hello")
"lohel"
```

**Solution:**
```
>> def rotate(seq, r) {
..   return aggregate(select((indices + r) % length, indices, ==), seq);
..   }
     console function: rotate(seq, r)
>> rotate(tokens, 1)("hello")
.. ;
         =  [o, h, e, l, l] (strings)
>> rotate(tokens, 2)("hello")
.. ;
         =  [l, o, h, e, l] (strings)
```

**Problem 3:**
Write a function that takes a sequence as input and "swaps every letter with its neighbor".
Specifically, for every even index $i$, positions $i$ and $i+1$ will be swapped;
if the length of the sequence is odd, then the last element should not move.
For example:
```
> swap(tokens)("hello")
"ehllo"
> swap(tokens)("ababab")
"bababa"
```

**Problem 4:**
Write a function that returns the maximum value in the sequence repeated for every position.
For example:
```
> maxseq(tokens)("ababcabab")
"ccccccccc"
```

~~**Problem 5:**
Write a function that returns the maximum value in the sequnce only of the tokens seen so far.
For example:~~
```
> maxseq(tokens)("ababcabab")
"abbbccccc"
```

> *Hint:*
> The `mask_ag` selector is useful for any problem that is either "autogenerative" or using only tokens "seen so far".

**Problem 6:**
Write a function that performs sequence reversal "autogeneratively".
That is, it will take a sequence as input, and the sequence will contain a special token `$` that marks the "end of the prompt".
The text before the `$` should be unchanged, and the text after the `$` should be the text before the `$` reversed (this text represents the model's response to the prompt).
The code should be robuse to the case when the length of text after `$` is not the same as the length of text before `$`.
For example:
```
> reverse_ag(tokens)("hello$     ")
"hello$olleh"
> reverse_ag(tokens)("hello$ ")
"hello$o"
> reverse_ag(tokens)("hello$X")
"hello$o"
> reverse_ag(tokens)("hello$XXXXXXXXXX")
"hello$olleh     "
```

**Problem 6:**
Write a function that counts the number of times a certain token appears in the input sequence.
For example:
```
> howmany(tokens, "a")("hello")
"00000"
> howmany(tokens, "h")("hello")
"11111"
> howmany(tokens, "l")("hello")
"22222"
```

**Problem 7:**
Write a function that counts the number of times a certain token has appeared in the input sequence so far.
For example:
```
> howmany(tokens, "a")("hello")
"00000"
> howmany(tokens, "h")("hello")
"11111"
> howmany(tokens, "e")("hello")
"01111"
> howmany(tokens, "l")("hello")
"00122"
```

**Problem 8:**
Create your own "interesting" problem statement.
Write a function/s-op that solves this problem.