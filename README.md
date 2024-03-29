## Color Number

Models that predict race/ethnicity based on the name often formalize the problem as a classification problem (see Sood and Laohaprapanon 2018, etc.). However, if name is the only thing we know about a person, there is generally no unique mapping to a race/ethnicity. Instead, there is a distribution, e.g., XX% identify as White, YY% as Asian, etc. Posing the regression problem as a classification involves making one of two choices---classifying to the mode, which involves losing data, or keeping the training data in a way that there is no unique mapping between a name (string) and race (Sood and Laohaprapanon 2018 choose this option). (To get calibrated probability estimates, the training data needs to be a random sample of the population though calibration for less popular names is likely to be poor given variability stemming from sampling.) A simpler (better) way to formalize the problem is to formalize it as a multi-value regression problem --- predict the race/ethnic distribution of each name. Using the Florida Voting Registration Data for 2022, we estimate a set of models that predict the distribution of race/ethnicity per name.

Our y variable is multi-output:

p_asian, p_white, p_black, p_hispanic, p_other

Our input variable is the name string. 

After estimation, we normalize the outputs for it to sum of 1.

We produce the data by grouping data by last_name and producing the data. We then split the data into train/test at 80/20. We use a loss function that is the mean absolute squared loss. (We also try L1Loss and cross-entropy loss.) We fit a MLP, LSTM, and a transformer model to predict the distribution of probabilities. 

## Todo

We compare how treating the same problem as a classification problem leads to performance differences in the performance metric of interest: mean absolute difference to the underlying prob. distribution. (We also try cross-entropy.)

### Scripts

* [MLP](notebooks/multioutput_regressor_lastname_mlp.ipynb)
* [LSTM](notebooks/multioutput_regressor_lastname_lstm.ipynb)
* [Transformer](notebooks/multioutput_regressor_lastname_transformer.ipynb)

### Authors

Gaurav Sood
