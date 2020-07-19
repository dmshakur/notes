# Pyspark ALS Notes

### Class methods
* `load(sc, path)`: Loads a model from a given path.
* `predict(user, product)`: Predicts rating for the given user and product.
* `predictAll(user_product)`: Returns a list of predicted ratings for input user and product pairs.
* `productFeatures()`: Returns a paired RDD, where the first element is the product and the second is an array of features corresponding to that product.
* `rank`: Rank for the features in this model.
* `recommendProducts(user, num)`: Recommends the top "num" products for a given user and returns a list of Rating objects sorted by the predicted rating in descending order.
* `recommendProductsForUsers(num)`: Recommends the top "num" number of products for all users. The number of recommendations returned per user may be less than "num".
* `recommendUsers(product, num)`: Recommends the top "num" number of users for a given product and returns a list of ratings objects sorted by the predicted rating in descending order.
* `recommendUsersForProducts(num)`: Recommends the top "num" number of users for all products. The number of recommendations returned per product may be less than "num".
* `userFeatures()`: Returns a paired RDD, where the first element is the user and the second is an array of features corresponding to that user.

### Class method `train`
Class method

`ALS.train(ratings, rank, iterations = 5, lambda_ = 0.01, blocks = -1, nonnegative = False, seed = None)`

Train a matrix factorization model given an RDD of ratings by users for a subset of products. The ratings matrix is approximated as the product of two lower-rank matrices of a given rank (number of features). To solve for these features, ALS is run iteratively with a configurable level of parallelism.
#### Parameters
* `ratings`: RDD of rating or (userID, productID, rating) tuple.
* `rank`: Number of features to use (also referred to as the number of latent factors).
* `iterations`: Number of iterations of ALS. (default 5)
* `lambda_`: Regularization parameter. (default: 0.01)
* `blocks`: Number of blocks used to parallelize the computation. A value of -1 will use an auto-configured number of blocks. (default: -1)
* `nonnegative`: A value of `True` will solve least-squares with non-negativity constraints. (default: `False`)
* `seed`: Random seed for initial matrix factorization model. A value of `None` will use system time as the seed. (default: None)

### Class method `trainImplicit`
Class method

`AlS.trainImplicit(ratings, rank, iterations = 5, lambda_ = 0.01, blocks = -1, alpha = 0.01, nonnegative = False, seed = None)`

Train a matrix factorization model given an RDD of 'implicit preferences' of users for a subset of products. It is the same as `train` otherwise.

#### Parameters
* `alpha`: A constant used in computing confidence.
All other parameters are the same as `train`.

## `pyspark.mllib.recommendation.Rating
Represents a (user, product, rating) tuple.
