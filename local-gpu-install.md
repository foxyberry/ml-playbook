Need to install GPU in Apple M3 Pro chip

```
pip install tensorflow-macos
pip install tensorflow-metal
```


```python
from tensorflow.python.client import device_lib
print(device_lib.list_local_devices())
```


To use GPU
```python
import tensorflow as tf

# GPU에서 연산이 실행되도록 설정
with tf.device('/GPU:0'):
    # CNN 모델 정의 및 연산 코드
    model = ...  # 예시 코드
    model.fit(...)
```

To use CPU
```python
import tensorflow as tf

# CPU에서 연산이 실행되도록 설정
with tf.device('/CPU:0'):
    # CNN 모델 정의 및 연산 코드
    model = ...  # 예시 코드
    model.fit(...)
```
