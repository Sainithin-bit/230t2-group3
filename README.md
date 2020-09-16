# 230T2 - Deep Learning for Time Series project

This repository includes the different work files of the project that was conducted as part of the requirements for 230T2 courses.
The paper that is replicated is the following: Constructing Financial Sentimental Factors in Chinese Market Using Natural Language Processing, available on ArXiv [here](https://arxiv.org/pdf/1809.08390v1.pdf).

The requirements for the project can be installed through the following command line:
> $ pip install -r requirements.txt

## Part 1: data retrieval and data engineering

This part focuses on getting the data and inputting it into a dataframe for easier manipulation in the next steps of the projects. The data set is included in the folder `reuters`.

The code in the notebook is also taking care of performance retrieval and labelling of the different headlines.

The notebook is named `230T2-data-exploration.ipynb`.

## Part 2: benchmark model

This part focuses on training naïve bayes classifier with tf-idf features, and compute the correlation of various benchmark variables with S&P500 price/returns. 

The data set is included in the folder `data`

The notebook is named is `230T2-baseline-model.ipynb`

## Part 3: BERT model

This part is dedicated to using the data that was preprocessed in the first section and to train the final layer of a BERT model to have access to sentimental analysis.

The requirements are already including in the top of this document.

The notebook is named `230T2-bert-model.ipynb`.

## Part 4: backtest strategy

In order to simulate predictive prowess of the sentiment factor calculated above, we implement a simple paper portfolio backtest strategy. There were quite a few alternatives in order to implement paper portfolios. 

We calculate the sentiment signal based on the previous 20 days for a given day. Then we adjust by bias, and take sign of signal where we buy if signal > 0 and sell if signal < 0. We hold for one day and calculate daily pnl without transaction cost. With these returns we assess performance of the sentiment signal such as mean, vol, sharpe ratio.

Few of the things we came up with were:

- Act on the instantaneous sentiment signal calculated everyday,
    - Hold for 1 day
    - Hold for 5 days
-  Act o the instantaneous sentiment signal, calculated based on weighting given to different news depending on its impact on a given day
    - Act on the Momentum of the sentiment signal
        - Transact S \& P 500
        - Transact VIX
    - Act on the persistent sentiment signal (rolling average of X days)
        - Transact S \& P 500
        - Transact VIX

The notebook is named `230T2-backtest-strategy.ipynb`.
