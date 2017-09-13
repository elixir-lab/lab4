# Hangman—Running the Dictionary as an Agent

Have a look at the code that implements the dictionary. Right now it
is a simple module. Each time you call `random_word`, it first reads the
word list from disk, then selects either a random word or all words of
a certain length. It has no ability to store any state, and therefore
has to read the word list afresh on each call.

Your mission is to change the dictionary so that it reads the
word list just once, and keeps that state in a named process. 
When you later call Dictionary.random_word, it should run the selection in that agent, using the already loaded word list.

Although you _could_ write this using `spawn`, in the real world we'd
exploit the convenience of the built-in libraries. In this case, I'd
like you to keep the word list in an Agent, and have the `random_word`
function invoke this agent.

Because the agent needs to be started, you'll need to implement a new
function, `start_link`. This will take an optional parameter, the name
of the word list. It will create an Agent containing the words in that
file. This agent will have the name `:dictionary`. I like to keep
things like server names in module attributes, and you'll find I've
already added

    @me :dictionary
    
to the WordList module.

Because `start_link` is part of the interface of the dictionary, we
need to first write a delegate in `lib/dictionary.ex` and then
implement it in lig/dictionary/word_list.ex`

Remember to run the test.
