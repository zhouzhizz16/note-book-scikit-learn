# Ridge Regression（岭回归）

Ridge Regression（岭回归）
岭回归用于处理下面两类问题：

1.数据点少于变量个数

2.变量间存在共线性

变量间存在共线性是，最小二乘回归得到的系数不稳定，方差很大，
这是因为系数矩阵x与它的转置矩阵相乘得到的矩阵不能求逆，
而ridge regression通过引入lamda参数，使得该问题得到解决

实质上是一种改良的最小二乘估计法，通过放弃最小二乘法的无偏性，
以损失部分信息、降低精度为代价，获得回归系数更为符合实际、
更可靠的回归方法，对病态数据的耐受性远远强于最小二乘法。

缺点：通常岭回归方程的R平方值会稍低于普通回归分析，
但回归系数的显著性往往明显高于普通回归，
在存在共线性问题和病态数据偏多的研究中有较大的实用价值。

遇到列向量相关的情形，岭回归是一种处理方法，
也可以用主成分分析PCA来进行降维

定义位于sklearn/linear-model/ridge.py下的
class Ridge(_BaseRidge, RegressorMixin):
继承 _BaseRidge 和 RegressorMixin

class Ridge(_BaseRidge, RegressorMixin)
继承 _BaseRidge 和 RegressorMixin
可应付多变量回归问题

_BaseRidge 在 ridge.py 内

## 参数
```
alpha : {float, array-like}
        shape = [n_targets] #小的正值alpha减小估计方差
normalize : boolean, optional, default False
copy_X : boolean, optional, default True (复制X数据,以防覆盖)
fit_intercept : boolean
tol : float
        Precision of the solution.
solver : {'auto', 'svd', 'cholesky', 'lsqr', 'sparse_cg'}

        - 'auto' 自动
        - 'svd' SVD分解计算系数. More stable for singular matrices than
          'cholesky'.
        - 'cholesky' scipy.linalg.solve 获得近似解. # w = inv(X^t X + alpha*Id) * X.T y
        - 'sparse_cg' 共轭梯度法,由于采用迭代,在大数据量时比'cholesky'更合适
          (possibility to set `tol` and `max_iter`).
        - 'lsqr' 最小二乘
          scipy.sparse.linalg.lsqr. It is the fatest but may not be available
          in old scipy versions. It also uses an iterative procedure.

## LinearRegression 类属性
coef_ : array, shape (n_features, ) or (n_targets, n_features)
        Estimated coefficients for the linear regression problem.

intercept_ : array
        Independent term in the linear model.
```

## 方法
```
Ridge.fit(X, y, sample_weight=None) #拟合数据

 X : {array-like, sparse matrix}, shape = [n_samples, n_features]
            Training data
 y :  array-like, shape = [n_samples] or [n_samples, n_targets]
            Target values

 sample_weight : float or numpy array of shape [n_samples]

 returns an instance of self.



```

## 示例
```

regr = linear_model.LinearRegression() # Create linear regression object


regr.fit(diabetes_X_train, diabetes_y_train) # Train the model using the training sets


print('Coefficients: \n', regr.coef_) # The coefficients

print("Residual sum of squares: %.2f"
      % np.mean((regr.predict(diabetes_X_test) - diabetes_y_test) ** 2)) # The mean square error

print('Variance score: %.2f' % regr.score(diabetes_X_test, diabetes_y_test)) # Explained variance score: 1 is perfect prediction
# score returns the coefficient of determination R^2 of the prediction
# The coefficient R^2 is defined as (1 - u/v), where u is the regression sum of squares ((y_true - y_pred) ** 2).sum() and
# v is the residual sum of squares ((y_true - y_true.mean()) ** 2).sum(). Best possible score is 1.0, lower values are worse.

```
    

