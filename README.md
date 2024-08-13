# WeirdR - Why I love R

*Some notes derviced from a 2024 userR! Conference [talk](https://www.youtube.com/watch?v=KOQBfC1WPwM) by Kelly Bodwin*

I like programming, but I wouldn't claim to be a computer programmer.

R is freedom. Its open-source, and the philosophy of open-source is "I will give you the code, please use it responsibly."

I think what bothers computer programmers with R is *how much* freedom we're given.

R's advanced coding features where code can be dynamically evaluated or modified could be used nefariously: e.g. *code obfuscation, data manipulation, unathorized data access, hidden code*

But, from the perspective a non-programmer, it will let us perform magic sorcery. 

And the community is the creative magic that makes me love R.

Statistical analysis? Art? Presentations? Dyanmic documents? APIs? R is for the useR.

## Non-standard Evaluation

    “Flexibility in syntax, if it does not lead to ambiguity, would seem a reasonable thing to ask of an interactive programming language.”

    — Kent Pitman

In the R ecosystem, code exists in two states: first as an 'expression' - a blueprint of intent, and then as a 'value' - the outcome of that intent. These expressions can be thought of as 'promises' or 'deferred actions', waiting to be fulfilled at a later time.

In most programming languages, you can only access the values of a function’s arguments. In R, you can also access the code used to compute them. This is typically the most surprising feature of R for those coming from another programming language.

This gives us the power to use unquoted variable names, looks cleaner, and makes it easy both perform iterative data analysis and let users write plain text that we can sanitize and convert to code.

## R is not 0-indexed

This is unorthodox compared to other programming languages, but it feels human. R is for statistics after all.

## R is not strongly typed

Everything is a list.  For example, create a vector of the alphabet. 

The first element of that vector isn't "a", but a vector of length 1 where the 1st element is the letter "a", and that vector's 1st element isn't actually the letter "a" but another vector of length 1 where the 1st element is the letter "a", etc...

And a vector is just a special list. Data frames? List of vectors. Plots? List of vectors. So everything is lists of lists, and this changed the way I think about data. For example [check out these guys](https://tiledb.com/).

## R is dynamic

There are three different assignment operators: two of them have leftwards and rightwards forms.

This is because R creates a global environment, typically known as the *user's workspace*. A new function means a new environment, and chain of enclosures. You can even influence the global environment from within a sub-environment too. 

This is useful for package creators, and R gives us the freedom to bounce around different environments passing and defining things in elegant ways.

## Object-oriented Programming

This isn't weird for programming, but is worth mentioning. The same function produces different output based on the type of object its given.

Summarizing a dataframe will give a six number summary of the dataframe. Summarizing a model will give you the coefficients, residuals, etc.

How does that [work](https://www.rdocumentation.org/packages/base/versions/3.6.2/topics/environment)? R will tell us that 'summary' is a function with a list of arguments (object, ...) for which R will perform 'UseMethod("summary") aka a method called "summary".

This is saying - 'hey, look around for the proper method for whatever object you were handed and use that', and it lets us do magic.

Lets say we create a model. Then we unclass it and call summary. Since everything is a list, R doesn't call the model summary anymore, but the list summary. 

We can take that object and assign it our own class and then write our own summary. 

class(mod) <- "kelly"
summary.kelly <- function(x) {
   print("Kelly is the best!")
   }
summary(mod)

"Kelly is the best!"
