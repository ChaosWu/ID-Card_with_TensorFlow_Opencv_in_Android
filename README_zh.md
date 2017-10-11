ID-Card_with_TensorFlow_Opencv_in_Android
==============================
## 涉及技术或者开源库
![t](./img/t.png)

# Environment
#### 1 centos 7
#### 2 [android studio](http://pan.baidu.com/s/1o8yB1wu)
#### 3 [NDK r10e](http://pan.baidu.com/s/1pLlImtt)(推荐) or [NDK r12](http://pan.baidu.com/s/1eSr0kLW)
#### 4 SDK
#### 5 JDK 1.8


# download tensorflow-sdk and opencv-sdk
#### 1 可以直接下载[tensorflow-sdk](http://pan.baidu.com/s/1jHQTDkE) 
也可以自己编译tensorflow android "static lib". 步骤如下：

按照[tensorflow_android](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/android/README.md)说明执行，并安装bazel等。

在[WORKSPACE](https://github.com/tensorflow/tensorflow/blob/master/WORKSPACE)中 配置SDK 和 NDK（bazel 编译时NDK 最好选择 r10e,NDK r12 就不行)
```
android_sdk_repository(
    name = "androidsdk",
    api_level = 23,
    build_tools_version = "23.0.1",
    # Replace with path to Android SDK on your system
    path = "<PATH_TO_SDK>",
)
android_ndk_repository(
    name="androidndk",
    path="<PATH_TO_NDK>",
    api_level=21)
```

在[BUILD](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/BUILD)中配置cpu平台

```
config_setting(
  name = "android_arm",
  values = {
    "crosstool_top": "//external:android/crosstool",
    "android_cpu": "armeabi-v7a",
  },
  visibility = ["//visibility:public"],
)
```


#### 2 下载[opencv-sdk](http://sourceforge.net/projects/opencvlibrary/files/opencv-android/3.1.0/OpenCV-3.1.0-android-sdk.zip/download)

#### 3 仔细阅读Opencv.mk 和 tensorflow_android.mk
tensorflow_android.mk这个是我写的，可能有bug,在arm平台是没有问题的

#### 4 [Android.mk](./jni-build/jni/Android.mk)
修改 opencv-sdk 和 tensorflow-sdk .mk 的包含目录
```
#this is my path, change it to yours
#opencv
include /home/centos/sdk/OpenCV-android-sdk/sdk/native/jni/OpenCV.mk

#tf-android
 include /home/centos/sdk/tensorflow-sdk/sdk/native/jni/tensorflow_android.mk
```

# use it
![这是我的Android Studio](./img/as.png)

执行ndk-build. 这里使用make包装了一下。真正的命令可以在[Makefile](./jni-build/Makefile)中查看
#### 1 open Terminal
#### 2 cd jni-build
#### 3 make
#### 4 make install

![执行过程](./img/command.png)

# examples
手机截图，红米3. Android 5 以上设备均支持
### RESULT
![my Id](./img/1000000.png)
![result](./img/1000001.png)
![result](./img/1000002.png)
![result](./img/1000003.png)
![result](./img/1000004.png)
![result](./img/1000005.png)
![result](./img/1000006.png)

#### more result in img/
### NEW UI
![new ui](./img/newUI.png)
