# CI2024_lab2
The first thing to say about this lab is that I have spent a lot of time trying to make the code work but the results were not satisfying. The errors I got were alternatively from my crossover function and from the cost function. 

The main problem was that after the generation of the offspring and the extension of the population, the cost function needed to prune the population to its default size ($100$) but some individuals were not acceptable in the sense that some paths did not return to the starting city (due to my bad crossover function or to the mutation function) or some paths did not cover the whole cities. This problem was faced by not accepting invalid solutions coming out from the crossover phase. However, the achived results are worse than the one found in the Teacher's Wolfram Notebook.

## Algorithm structure
In the first phase, the goal was to integrate *Partially-Mapped Crossover* to the Evolutionary Algorithm, but after I managed to code it, many errors about buggy indexing convinced me to change the crossover type, favouring *Inver-Over Crossover*. 

Initially I tried running it starting from a randomized popoulation of paths, but following the Teacher's  advice I decided to start from the initial **Greedy solution** provided by his code, mutating it by adding some randomness (shuffling segments made by $10$ elements of the paths) in order to start from a population that was not random, neither simply greedy.

The population was firstly anlyzed with the cost function and then the *Parent Selection* was implemented with a **Fitness-Proportional selection** that selected 50 parents from the population with a Roulette Wheel based on the weights given by the cost function (the higher the cost, the lower the probability to be selected as parent). 

Then, the *Inver-Over Crossover* was integrated in this way: with a probability of $0.2$, the crossover was just taking a segment from the first parent and reverse it in the offspring, while in the other case the second parent was used to do the actual Inver-Over operation. 

After the crossover, the generated offspring was mutated with *Insert Mutation* with a probability of $0.5$. The population was then extended with the offspring and successively pruned with *Survivor selection* based on **Fitness-Proportional selection**. The best results for the different datasets were: 
| Cities | Best cost found|
|----------|----------|
| Italy | 5783 |
| China | 73026 |
| Russia | 48749.33 |
| US | 63637.35 |
| Vanuatu | 1345.54 |
