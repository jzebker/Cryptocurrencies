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
• An elbow curve is created using hvPlot to find the best value for K

`# Create an elbow curve to find the best value for K.
# Create empty list and our range of K values
inertia = []
k = list(range(1, 11))
# Looking for the best K
for i in k:
    km = KMeans(n_clusters=i, random_state=0)
    km.fit(pcs_df)
    inertia.append(km.inertia_)
# Define a DataFrame to plot the Elbow Curve using hvPlot
elbow_data = {"k": k, "inertia": inertia}
df_elbow = pd.DataFrame(elbow_data)
df_elbow.hvplot.line(x="k", y="inertia", title="Elbow Curve", xticks=k)`

<p align='center'>
  <img src='https://github.com/jzebker/Cryptocurrencies/blob/main/img/CoinNameDF.png?raw=true'>
</p>

• Predictions are made on the K clusters of the cryptocurrencies’ data 

`# Initialize the K-Means model.
model = KMeans(n_clusters=4, random_state=0)

# Fit the model
model.fit(pcs_df)

# Predict clusters
predictions = model.predict(pcs_df)`

• A new DataFrame is created with the same index as the crypto_df DataFrame and has the following columns: Algorithm, ProofType, TotalCoinsMined, TotalCoinSupply, PC 1, PC 2, PC 3, CoinName, and Class

<p align='center'>
  <img src='https://github.com/jzebker/Cryptocurrencies/blob/main/img/CoinNameDF.png?raw=true'>
</p>

## Deliverable 4: Visualizing Cryptocurrencies Results
• The clusters are plotted using a 3D scatter plot, and each data point shows the CoinName and Algorithm on hover

• A table with tradable cryptocurrencies is created using the hvplot.table() function

• The total number of tradable cryptocurrencies is printed

• A DataFrame is created that contains the clustered_df DataFrame index, the scaled data, and the CoinName and Class columns 

• A hvplot scatter plot is created where the X-axis is "TotalCoinsMined", the Y-axis is "TotalCoinSupply", the data is ordered by "Class", and it shows the CoinName when you hover over the data point

