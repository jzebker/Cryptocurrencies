# Cryptocurrencies
## Overview
Create an analysis for your clients who are preparing to get into the cryptocurrency market that includes what cryptocurrencies are on the trading market and how they could be grouped to create a classification system for this new investment.
## Deliverable 1: Preprocessing the Data for PCA
• All cryptocurrencies that are not being traded are removed
`crypto_df = crypto_df.loc[crypto_df['IsTrading'] == True]`
• The IsTrading column is dropped
`crypto_df = crypto_df.drop(['IsTrading'],axis=1)`
## Deliverable 2: Reducing Data Dimensions Using PCA
## Deliverable 3: Clustering Cryptocurrencies Using K-means
## Deliverable 4: Visualizing Cryptocurrencies Results
## Summary
