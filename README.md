# MultinomialCIProject2020

The goal of this project is the predict results in 2020 U.S. presidential election.
With more mail-in ballots were used due the COVID pandemic, 
as well as different rhetoric on mail-in ballots from both sides, 
mail-in ballots will have different characteristics than in-person ballots,
and there could even be differnece between mail-in ballots that were delivered in different methods.

The project relies on good and clean data. The data used here are from New York Times' election coverage.
However, the quality of the data can only be as good as it is originally submitted.
While all states have county breakdown (an absolute must), not all county have mail-in ballots breakdown.
To overcome this issue, this project can keep multiple snapshots when data were pulled.
We then can use the change in votes to make any meaningful prediction.
But when it is not possible, we can only rely on using all votes to predict the final outcome, 
which almost guarantee inaccurate prediction unless mail-in votes behave similarly than the rest.

Another issue is the accuracy of expected remaining votes. 
This data were provided by NYT but were not guaranteed to be accurate.
In fact, the expected remaining votes often changed as NYT received more information.
Since I don't think my remaining votes estimate is any better, we can only rely on NYT's estimate.

When all data were ready, it uses a 2-step confidence interval (CI) prediction interval (PI) process.
It uses [`MultinomialCI` package](https://cran.r-project.org/web/packages/MultinomialCI/index.html).

1. Using each candidates vote counts, `MultinomialCI` will give a CI for the probability of a vote cast to a particular candidate.
For each county and each candidate, it will output a low probability and a high probability.
2. With each of the low and high probability, a PI is calculated based on the expected remaining votes.
The lower range of the PI from the low probability will be the low end of a candidate,
and the upper range of the PI from the high probaility will be the high end of a candidate.
3. The final margin is calculated using one candidate's low end minus the other candidate's high end, and vice versa.

Since vote counting will not last forever (hopefully), data were archived when I ran the program and they were included in this repo. You can see a sample output in [countyCI.pdf](countyCI.pdf).
