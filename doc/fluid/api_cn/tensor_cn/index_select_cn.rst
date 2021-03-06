.. _cn_api_tensor_search_index_select:

index_select
-------------------------------

.. py:function:: paddle.index_select(x, index, axis=0, name=None)

:alias_main: paddle.index_select
:alias: paddle.index_select,paddle.tensor.index_select,paddle.tensor.search.index_select



该OP沿着指定维度 ``axis`` 对输入 ``input`` 进行索引，取 ``index`` 中指定的相应项，然后返回到一个新的张量。这里 ``index`` 是一个 ``1-D`` 张量。除 ``axis`` 维外，返回的张量其余维度大小同输入 ``input`` ， ``axis`` 维大小等于 ``index`` 的大小。
        
**参数**：
    - **x** （Variable）– 输入张量。x的数据类型可以是float32，float64，int32，int64。
    - **index** （Variable）– 包含索引下标的一维张量。
    - **axis**    (int, optional) – 索引轴，若未指定，则默认选取第0维。
    - **name** （str，可选）- 具体用法请参见 :ref:`api_guide_Name` ，一般无需设置，默认值为None。

**返回**：
    -**Variable**: 数据类型同输入。
     
抛出异常：
    - ``TypeError`` - 当x或者index的类型不是Variable。
    - ``TypeError`` - 当x的数据类型不是float32、float64、int32、int64其中之一或者index的数据类型不是int32、int64其中之一。


**代码示例**：

.. code-block:: python

        import paddle
        import numpy as np

        paddle.enable_imperative()  # Now we are in imperative mode
        data = np.array([[1.0, 2.0, 3.0, 4.0],
                         [5.0, 6.0, 7.0, 8.0],
                         [9.0, 10.0, 11.0, 12.0]])
        data_index = np.array([-1, 1, 1]).astype('int32')

        x = paddle.imperative.to_variable(data)
        index = paddle.imperative.to_variable(data_index)
        out_z1 = paddle.index_select(x=x, index=index)
        #[[1. 2. 3. 4.]
        # [5. 6. 7. 8.]
        # [5. 6. 7. 8.]]
        out_z2 = paddle.index_select(x=x, index=index, axis=1)
        #[[ 1.  2.  2.]
        # [ 5.  6.  6.]
        # [ 9. 10. 10.]]

