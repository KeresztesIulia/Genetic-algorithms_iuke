# Genetic algorithms_iuke
 A university project to build a genetic algorithm. Can only calculate built-in mathematical functions.

# About the genetical algorithm

## Chromosome class data

**genes (list of floats)**  
Parameters for the mathematical function.

**function_value**  
Return value of the mathematical function for the parameters contained in the genes.

**fitness**  
$\frac{1}{function\_ value} \rightarrow$ the individual with the lowest function value will be deemed fittest, since we're trying to find the minimum value of the mathematical function.

**diversity**  
The sum of Euclidean distances from the other chromosomes in the current generation's population.

**probability**  
The probability used for the selection phase.
This is calculated based on the used genetic algorithm object's probability_method and P parameters (detailed later).

**rank**  
Rank of the chromosome in the generation.
Calculated based on the used generic algorithm object's probability_method parameter (detailed later).

**chromosome comparison operators**  
The operators <, >, <=, >= are overloaded for the class in a way that it compares the fitness values of the objects. Equality (==)/non-equality (!=) compares all the data of the objects (genes, probability etc.).

## GeneticAlgorithm class data

**fitness_function**  
The mathematical function of which minimal value we want to estimate. Built-in options:
- Booth: $f(x,y) = (x+2y-7)^2+(2x+y-5)^2$
- Rastgirin: $f(X) = An + \sum_{i=1}^{n} [x_i^2 - A \cos(2\pi x_i)]$
- Lévi: $f(x,y) = \sin^23\pi x + (x-1)^2(1+\sin^23\pi y)+(y-1)^2(1+sin^22\pi y)$

**probability_method**  
The method to use for calculating the selection probability of chromosomes. Can be relative, based on fitness rank or based on diversity and fitness rank.

**selection_method**  
The method tu use for the selection of the parents. Options:
- roulette: parents are chosen at random based on the probability calculated previously.
- tournament: an amount of individuals (set by the contestants parameter) are chosen at random with the same chance; the individuals with the best fitness value are selected as parents
- SUS (Stochastic Universal Sampling): we assign distances to individuals based on their probability, then generate a number in the [0, 1/n) interval (where n is the number of parents we want to have). The individual matching the distance generated will be the first parent, after which we add 1/n to the distance as many times as we need to have the number of parents we aim for

**mutation-method**  
The type of mutation to apply to chromosomes (in case it mutates at all). The options are:
- one: if a chromosome mutates, only one of its genes will mutate
- all: if a chromosome mutates, all of its genes will mutate
- any: for every gene, whether it mutates or not is decided separately; thus, any number of genes might mutate, even none or all

**A**  
The A value needed for the Rastrigin function.

**P**  
Base probability to use for calculating probabilities of chromosomes in the case of fitness or diversity and fitness ranking.

**contestants**  
The number of contestants that should participate in a tournament, in case of using that as the selection method. Default value is 2. Max value is the population ssize - 1.

**min_gene_value**, **max_gene_value**  
Closed interval for the values of the genes.

**crossover_points**  
The number of crossover points. Minimum value: 1. Maximum value: gene count - 1.

**elite_count**  
The size of the elite population.

**elite_pool**  
The size of the elite pool. Not the same as the elite population: the parents for the next generation will only be chosen from among this pool. The other individuals of the generation are discarded. It's advise to only leave out a small percentage of the population. Set to 0 to disable elite pooling.

**elite_mutation_rate**  
The probability of elite individuals mutating before getting added to the new generation.

**mutation_rate**  
The probability of child individuals mutating.

**mutation_amount**  
The maximum amount with which to change (either increase or decrease) a gene when mutating.

**mutation_decay**  
An experimental value from the [0, 1] interval. If less than 1, mutation rates for both elite and child individuals will decrease with each generation, down to the percentage given by this value.