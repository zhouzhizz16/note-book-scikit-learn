# Ordinary least squares Linear Regression（普通最小二乘）

标签（空格分隔）： 普通最小二乘线性回归

---
## 代码结构
sklearn/linear-model/base.py 文件中
 **LinearRegression**类是最外层接口，继承自**LinearModel**和**RegressorMixin**两个类
### paramters
-------------
>* fit_intercept : bool 是否拟合截距项，false 无截距项,default True
>* normalize : bool 数据是否需要标准化 ，true 会进行标准化处理,default False
>* copy_X : 传入LinearRegression fit 方法的X 是否需要复制，如果False ,传人的参数会别修改，default True
>* n_jobs 过时，1.7之后删除此参数，defalut 1

### fit 函数，这个方法只是对 scipy 中的方法的封装。并没多少算法的细节
-----------
```python
def fit(self, X, y, n_jobs=1):
        """
        X : numpy array or sparse matrix of shape [n_samples,n_features]
            Training data
            
        y : numpy array of shape [n_samples, n_targets]
            Target values

        Returns
        -------
        self : returns an instance of self.
        """
        #删除对n_jobs 的检查
        
        #检查输入数据是否有效
        X, y = check_X_y(X, y, accept_sparse=['csr', 'csc', 'coo'],
                         y_numeric=True, multi_output=True)
        #计算 数据均值标准差，数据标准化
        X, y, X_mean, y_mean, X_std = self._center_data(
            X, y, self.fit_intercept, self.normalize, self.copy_X)
        
        if sp.issparse(X):  ##如果X 是稀疏矩阵
            if y.ndim < 2:  ## target 的维度小余2
                out = sparse_lsqr(X, y)  ##直接调用 scipy 中的sparse_lsqr 拟合
                self.coef_ = out[0] ##参数
                self.residues_ = out[3]  
            else:      ##TODO 没懂target 会有多个维度？
                # sparse_lstsq cannot handle y with shape (M, K)
                outs = Parallel(n_jobs=n_jobs_)(
                    delayed(sparse_lsqr)(X, y[:, j].ravel())
                    for j in range(y.shape[1]))
                self.coef_ = np.vstack(out[0] for out in outs) ##coef_ 继承自父类
                self.residues_ = np.vstack(out[3] for out in outs)
        else:  #直接利用linalg.lstsq 
            self.coef_, self.residues_, self.rank_, self.singular_ = \
                linalg.lstsq(X, y)
            self.coef_ = self.coef_.T

        if y.ndim == 1:
            self.coef_ = np.ravel(self.coef_)
        self._set_intercept(X_mean, y_mean, X_std)
        return self  ## 返回自身
```

    

