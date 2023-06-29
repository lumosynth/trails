# The Gameplan

So, we need to break down exactly what we want to do.

Our end goal is to make an AGI known as Voxel, which has Chat Completions, like ChatGPT.

First, we must construct our dataset (Grapha).

Our possible sources for data include:

* Wikipedia
* Msgroom logs
* Scraped RSS feeds

Our dataset will be in shards, each no-less than 1GB, so we don't hit GitHub limits..

Next, we will generate our token library, Synthico, by having a token queue, which starts out with all the characters we know of, and then from there, we repeatedly sort the token list by common-ness, and then add the most common token to the final list, and then add the token + all the other letters to the queue, we do this until we have to top 100,000 most common tokens.

Finally, we add the meat of it, we train a model that extends text, by having a state update model, which updates the RNN's memory, and then the token outputer, that outputs a token and updates the RNN's memory, so we add all our input with the state update model, and then output it with the token outputter, until the token outputter outputs a special END token.

Then we create something similar to openai/evals, called discourse, which we will tune the model to, so it's ready for chatting. We also add some special tokens to prevent weirdness.
