Need to install GPU in Apple M3 Pro chip

```
pip install tensorflow-macos
pip install tensorflow-metal
```


```python
from tensorflow.python.client import device_lib
print(device_lib.list_local_devices())
```

```
[name: "/device:CPU:0"
device_type: "CPU"
memory_limit: 268435456
locality {
}
incarnation: 9668355588602698228
xla_global_id: -1
, name: "/device:GPU:0"
device_type: "GPU"
locality {
  bus_id: 1
}
incarnation: 11331360857699006507
physical_device_desc: "device: 0, name: METAL, pci bus id: <undefined>"
xla_global_id: -1
]
2024-10-21 21:18:05.635582: I metal_plugin/src/device/metal_device.cc:1154] Metal device set to: Apple M3 Pro
2024-10-21 21:18:05.635611: I metal_plugin/src/device/metal_device.cc:296] systemMemory: 36.00 GB
2024-10-21 21:18:05.635617: I metal_plugin/src/device/metal_device.cc:313] maxCacheSize: 13.50 GB
2024-10-21 21:18:05.635635: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:305] Could not identify NUMA node of platform GPU ID 0, defaulting to 0. Your kernel may not have been built with NUMA support.
2024-10-21 21:18:05.635652: I tensorflow/core/common_runtime/pluggable_device/pluggable_device_factory.cc:271] Created TensorFlow device (/device:GPU:0 with 0 MB memory) -> physical PluggableDevice (device: 0, name: METAL, pci bus id: <undefined>)
```

- /device:CPU:0와 /device:GPU:0이 나열되어 있습니다. 이는 TensorFlow가 CPU와 GPU 모두 인식했음을 의미합니다.
- GPU는 "METAL"로 표시되며, 이는 Apple의 Metal API를 통해 GPU를 사용하고 있다는 뜻입니다.
- systemMemory는 시스템 메모리가 36GB임을 나타내고, maxCacheSize는 GPU에서 사용할 수 있는 최대 캐시 크기가 13.5GB라는 것을 보여줍니다.
- 이는 TensorFlow가 NUMA (Non-Uniform Memory Access) 노드를 인식하지 못했다는 경고입니다. 하지만 이는 Apple Silicon에서 큰 문제가 되지 않습니다. NUMA는 주로 대규모 멀티코어 시스템에서 중요한데, Apple M 시리즈에서는 특별한 설정 없이도 GPU를 사용할 수 있습니다.


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
