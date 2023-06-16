## Color Number

Models that predict race/ethnicity based on the name often formalize the problem as a classification problem (see Sood and Laohaprapanon 2018, etc.). However, if name is the only thing we know about a person, there is generally no unique mapping to a race/ethnicity. Instead, there is a distribution, e.g., XX% identify as White, YY% as Asian, etc. Posing the regression problem as a classification involves making one of two choices---classifying to the mode, which involves losing data, or keeping the training data in a way that there is no unique mapping between a name (string) and race (Sood and Laohaprapanon 2018 choose this option). (To get calibrated probability estimates, the training data needs to be a random sample of the population though calibration for less popular names is likely to be poor given variability stemming from sampling.) A simpler (better) way to formalize the problem is to formalize it as a multi-value regression problem --- predict the race/ethnic distribution of each name. Using the Florida Voting Registration Data for 2022, we estimate a transformer model that predicts the distribution of race/ethnicity per name using the sequence of characters in a name.

Our y variable is multi-output:

p_asian, p_white, p_black, p_hispanic, p_other

We normalize the outputs for it to sum of 1.

Our input variable is the name string. 

We produce the data by grouping data by last_name and producing the data. We then split the data into train/test at 90/10. We use a loss function that is the mean absolute difference across the first 4 categories (to make sure we are not overweighting losses from categories with larger density, e.g., white and because the 5th category is completely explained by the other four). We then fit a transformer model that exploits the sequence of characters to predict the distribution of probabilities. We use dropout for estimating the uncertainty in our predictions.

We compare how treating the same problem as a classification problem leads to performance differences in the performance metric of interest: mean absolute difference across the first 4 categories. 

### Authors

Gaurav Sood
