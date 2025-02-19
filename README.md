tflite_micro_runtime
========================

This allows for running TF-Lite models on a RaspberryPi Zero using the Tensorflow-Lite Micro (TFLM) interpreter.  

This provides the Python package:`tflite_micro_runtime` which uses the same API as `tflite_runtime`. 
The main difference is `tflite_micro_runtime` uses the Tensorflow-Lite Micro interpreter instead of the 
Tensorflow-Lite interpreter.

Using the Tensorflow-Lite Micro (TFLM) interpeter provides __~8x improvement__ on inference time.  
TFLM provides a speedup because it uses the [ARM CMSIS NN](https://github.com/ARM-software/CMSIS_5/tree/develop/CMSIS/NN) library which is optimized for ARMv6 processor that RPI0 uses.
The RPI0's ARMv6 processor does not have a GPU or other hardware optimizations so can not leverage any of the features
that come with the `tflite_runtime` library. Thus the `tflite_micro_runtime` library is faster on the RPI0 but not other Raspberry PIs that do feautre a GPU.


More details on the `tflite_runtime` Python package here:  
https://www.tensorflow.org/lite/guide/python

More details on the Tensorflow-Lite Micro interpreter here:  
https://github.com/tensorflow/tflite-micro

__NOTE:__ This repo is a fork of the `tflite-micro` repo.



# Install

To install the `tflite_micro_runtime` Python package, run the PIP command on the RPI0:

```bash
pip3 install https://github.com/driedler/tflite_micro_runtime/releases/download/1.1.0/tflite_micro_runtime-1.1.0-cp37-cp37m-linux_armv6l.whl
```

# Build

To build the `tflite_micro_runtime` Python package, run the bash scripts in a Linux environment:

## Install Python3
```bash
# Install Python3.7, numpy, and pybind11
./tensorflow/lite/micro/tools/rpi0_pip_package/install_python37.sh
# OR Install Python3.9, numpy, and pybind11
./tensorflow/lite/micro/tools/rpi0_pip_package/install_python39.sh
```

## Build Python Package
```bash
# Build tflite_micro_runtime wheel
./tensorflow/lite/micro/tools/rpi0_pip_package/build_pip_package37.sh

# OR Build tflite_micro_runtime wheel
./tensorflow/lite/micro/tools/rpi0_pip_package/build_pip_package39.sh
```


# Runtime Comparison Script

A runtime comparsion script is available the compares the `tflite_micro_runtime` and `tflite_runtime` 
packages at: [./tensorflow/lite/micro/python/runtime_comparison.py](./tensorflow/lite/micro/python/runtime_comparison.py)

Refer to the comments at the top of the script for more details.
