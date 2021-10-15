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
  <img src='https://github.com/jzebker/Cryptocurrencies/blob/main/img/CoinNameDF.png?raw=true'>
</p>

• The get_dummies() method is used to create variables for the text features, which are then stored in a new DataFrame, X

`X = pd.get_dummies(crypto_df, columns = ["Algorithm","ProofType"])`

• The features from the X DataFrame have been standardized using the StandardScaler fit_transform() function

`X = StandardScaler().fit_transform(X)`

## Deliverable 2: Reducing Data Dimensions Using PCA
• The PCA algorithm reduces the dimensions of the X DataFrame down to three principal components

`pca = PCA(n_components=3)
crypto_pca = pca.fit_transform(X)`

• The pcs_df DataFrame is created and has the following three columns, PC 1, PC 2, and PC 3, and has the index from the crypto_df DataFrame

`pcs_df = pd.DataFrame(
    data=crypto_pca,columns=["PC 1", "PC 2", "PC 3"],
    index=crypto_df.index
)`

<p align='center'>
  <img src='https://github.com/jzebker/Cryptocurrencies/blob/main/img/CoinNameDF.png?raw=true'>
</p>

## Deliverable 3: Clustering Cryptocurrencies Using K-means
## Deliverable 4: Visualizing Cryptocurrencies Results
## Summary
