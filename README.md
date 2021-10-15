# Cryptocurrencies
## Overview
Create an analysis for your clients who are preparing to get into the cryptocurrency market that includes what cryptocurrencies are on the trading market and how they could be grouped to create a classification system for this new investment.
## Deliverable 1: Preprocessing the Data for PCA
• All cryptocurrencies that are not being traded are removed
`crypto_df = crypto_df.loc[crypto_df['IsTrading'] == True]`

• The IsTrading column is dropped
`crypto_df = crypto_df.drop(['IsTrading'],axis=1)`

• All the rows that have at least one null value are removed
`crypto_df = crypto_df.dropna()`

• All the rows that do not have coins being mined are removed
`crypto_df = crypto_df.loc[crypto_df["TotalCoinsMined"]>0]`

• The CoinName column is dropped
`crypto_df = crypto_df.drop(['CoinName'],axis=1)`

• A new DataFrame is created that stores all cryptocurrency names from the CoinName column and retains the index from the crypto_df DataFrame
`crypto_names = crypto_df.drop(['Algorithm','ProofType','TotalCoinsMined','TotalCoinSupply'],axis=1)`

<p align='center'>
  <img src=>
</p>

## Deliverable 2: Reducing Data Dimensions Using PCA
## Deliverable 3: Clustering Cryptocurrencies Using K-means
## Deliverable 4: Visualizing Cryptocurrencies Results
## Summary
