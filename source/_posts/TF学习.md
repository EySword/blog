# Keras流程

## 加载数据

```python
fashion_mnist=keras.datasets.fashion_mnist
(X_train_full,y_train_full),(X_test,y_test)=fashion_mnist.load_data()
```

## 构建模型

```python
model=keras.models.Sequential([
    keras.layers.Dense(10,activation='relu'),
    ...
])
model.add()#添加每一层
```

`model.summary()`显示所有层

`keras.utils.plot_model()`生成模型图像

`model.layers`获取模型层列表

`weights,biases = hidden1.get_weithts()`获取所有参数, 还有`get_weithts()`

## 编译模型

```python
model.compile(loss='sparse_categorial_crossentropy',
             optimizer='sgd',
             metrics=['accuracy'])
```

损失函数根据实际情况指定。且如果损失函数需要注意参数，应该用`optimizer=keras.optimizers.SGD(learning_rate=0.1)`来设置

## 训练和评估模型

```python
history=model.fit(X_train,y_train,epochs=30,
                 validation_data=(X_valid,y_valid))
```

验证集可以用`validation_split=0.1`来设置，意思是用最后10%做验证

如果训练集不平衡（某一类很多），调用`fit()`时可以用`class_weight`参数，减少多的项目的权重

`sample_weight`每个实例的权重

`fit()`返回一个History对象，包括训练参数`history.params`、经历的轮次列表`history.epoch`、损失和额外指标`history.history`

```python
pd.DataFrame(history.history).plot()
plt.grid(True)
plt.gca().set_ylim(0,1)
plt.show()
```

用`fit()`创建`pd.DF`并调用`plot()`来画图

调整参数

```python
model.evaluate(X_test,y_test)
```

在测试集上评估泛化误差

## 使用模型进行预测

```python
y_proba=model.predict(X_new)
```

