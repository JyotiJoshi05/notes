In statistics, the set of all individuals relevant to a particular statistical question is called a population.
A smaller group selected from a population is called a sample. When we select a smaller group from a population we do sampling.
The elements of a population referred to as individuals, units, events, observations. These are all used interchangeably and refer to the same thing: the individual parts of a population. When we use the term "population individuals", the population is not necessarily composed of people. "Individuals" here is a general term that could refer to people, needles, frogs, stars, etc.
sample unit, sample point, sample individual, or sample observation.
```
there's almost always some difference between the metrics of a population and the metrics of a sample. This difference can be seen as an error, and because it's the result of sampling, it's called sampling error.
```
A metric specific to a population is called a parameter, while one specific to a sample is called a statistic. In our example above, the average salary of all the employees is a parameter because it's a metric that describes the entire population. The average salaries from our two samples are examples of statistics because they only describe the samples.

Another way to think of the concept of the sampling error is as the difference between a parameter and a statistic:

sampling error = parameter - statistic
In statistical terms, we want our samples to be representative of their corresponding populations. If a sample is representative, then the sampling error is low. The more representative a sample is, the smaller the sampling error. The less representative a sample is, the greater the sampling error.
One way to perform random sampling is to generate random numbers and use them to select a few sample units from the population. In statistics, this sampling method is called simple random sampling, and it's often abbreviated as SRS.

A pseudorandom number generator uses an initial value to generate a sequence of numbers that has properties similar to those of a sequence that is truly random. With random_state we specify that initial value used by the pseudorandom number generator.

If we want to generate a sequence of five numbers using a pseudorandom generator, and begin from an initial value of 1, we'll get the same five numbers no matter how many times we run the code.

To ensure we end up with a sample that has observations for all the categories of interest, we can change the sampling method. We can organize our data set into different groups, and then do simple random sampling for every group. We can group our data set by player position, and then sample randomly from each group.
This sampling method is called stratified sampling, and each stratified group is also known as a stratum.
(Picking two players from each of five groups).

 let's say you want to analyze how people review and rate movies as a function of movie budget. There are a lot of websites out there that can help with data collection, but how can you go about it so that you can spend one day or two on getting the data you need, rather than one month or two?

One way is to list all the data sources you can find, and then randomly pick only a few of them to collect data from. Then you can sample individually each of the sources you've randomly picked. This sampling method is called cluster sampling, and each of the individual data sources is called a cluster.

Let's say you work for an e-commerce company that has a table in a database with more than 10 million rows of online transactions. The marketing team asks you to analyze the data and find categories of customers with a low buying rate, so that they can target their marketing campaigns at the right people. Instead of working with more than 10 million rows at each step of your analysis, you can save a lot of code running time by sampling several hundred rows, and perform your analysis on the sample. You can do a simple random sampling, but if you're interested in some categories beforehand, it might be a good idea to use stratified sampling.

Let's consider a different situation. It could be that you need to collect data from an API that either has usage limit, or is not free. In this case, you are more or less forced to sample. Knowing how and what to sample can be of great use.

Another common use case of sampling is when the data is scattered across different locations (different websites, different databases, different companies, etc.). As we've discussed in the previous screen, cluster sampling would be a great choice in such a scenario.

Sampling is a vast topic in statistics, and there are other sampling methods besides what we've discussed so far in our course. Here's a good starting point to read about other potentially useful sampling methods.

When we describe a sample or a population (by measuring averages, proportions, and other metrics; by visualizing properties of the data through graphs; etc.), we do descriptive statistics.

When we try to use a sample to draw conclusions about a population, we do inferential statistics (we infer information from the sample about the population).
Systematic sampling (also known as interval sampling) relies on arranging the study population according to some ordering scheme and then selecting elements at regular intervals through that ordered list.

 mean as being the value located at that particular point in the distribution where the total distance of the values below the mean is the same as the total distance of the values that are above the mean. In our last exercise, we saw that this holds true for the distribution [0,2,3,3,3,4,13].
 
 When estimating the population mean  using the sample mean , there are three possible scenarios:

The sample mean  overestimates the population mean . This means that .
The sample mean  underestimates the population mean . This means that .
The sample mean  is equal to the population mean . This means that 