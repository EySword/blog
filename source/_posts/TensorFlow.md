

## `tf.keras.Sequential`：创建一个`tf.keras.Model`的命令链

```py
model = tf.keras.Sequential()
model.add(tf.keras.layers.Dense(8, input_shape=(16,)))
# Afterwards, we do automatic shape inference:
model.add(tf.keras.layers.Dense(4))
```

## `tf.keras.layers`Public API for tf.keras.layers namespace

1. `tf.keras.layers.ZeroPadding2D`文档里没有`input_shape`这个选项，我没有添加的时候出现了*The layer has never been called and thus has no defined output shape*的报错，添加`input_shape=(64,64,3)`后解决

## `tf.data`

### [Dataset structure](https://www.tensorflow.org/guide/data#dataset_structure)

用于输入数据，可以用[`tf.TypeSpec`](https://www.tensorflow.org/api_docs/python/tf/TypeSpec)进行接收，包括`tf.Tensor`, `tf.sparse.SparseTensor`, `tf.RaggedTensor`, `tf.TensorArray`和`tf.data.Dataset`

可以接收的格式为 `tuple`, `dict`, `NamedTuple`,和 `OrderedDict`。注意，不包括`list`，因为In particular, `list` is not a valid construct for expressing the structure of dataset elements. This is because early tf.data users felt strongly about `list` inputs (e.g. passed to `tf.data.Dataset.from_tensors`) being automatically packed as tensors and `list` outputs (e.g. return values of user-defined functions) being coerced into a `tuple`.

#### tf.data.Dataset

```py
tf.data.Dataset.from_tensor_slices()
```

给定的张量沿着它们的第一维切片。该操作保留了输入张量的结构，去掉了每个张量的第一个维度，并将其作为数据集的维度。所有的输入张量在它们的第一维中必须有相同的大小。

## tensorflow.keras.preprocessing.image_dataset_from_directory

**What you should remember:**

- When calling image_data_set_from_directory(), specify the train/val subsets and match the seeds to prevent overlap
- Use prefetch() to prevent memory bottlenecks when reading from disk
- Give your model more to learn from with simple data augmentations like rotation and flipping.
- When using a pretrained model, it's best to reuse the weights it was trained on.