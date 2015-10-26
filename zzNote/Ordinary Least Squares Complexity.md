# Ordinary least squares Linear Regression（普通最小二乘）

Ordinary least squares Linear Regression（普通最小二乘）

定义位于sklearn/linear-model/base.py下的
class LinearRegression(LinearModel, RegressorMixin)
继承 LinearModel 和 RegressorMixin

## 参数
```
fit_intercept : boolean, optional
normalize : boolean, optional, default False
copy_X : boolean, optional, default True (复制X数据,以防覆盖)
n_jobs : int, optional, default 1

## LinearRegression 类属性
coef_ : array, shape (n_features, ) or (n_targets, n_features)
        Estimated coefficients for the linear regression problem.

intercept_ : array
        Independent term in the linear model.
```

## 方法
```
LinearRegression.fit(self, X, y, n_jobs=1) #拟合数据

 X : numpy array or sparse matrix of shape [n_samples,n_features]
            Training data
 y : numpy array of shape [n_samples, n_targets]
            Target values

 returns an instance of self.


 X, y, X_mean, y_mean, X_std = self._center_data(
            X, y, self.fit_intercept, self.normalize, self.copy_X)#数据中心化
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
    

