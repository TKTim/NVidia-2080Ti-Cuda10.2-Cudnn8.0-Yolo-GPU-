安裝程序
=
* [下載driver](#下載driver)
* [下載CUDA toolkit = CUDA](#下載CUDA-toolkit=CUDA)
* [下載Cudnn](#下載Cudnn)
* [下載YOLO](#下載YOLO)
* [下載Opencv](#下載Opencv)
* [架設最終YOLO](#架設最終YOLO)


下載driver
=

```
# ubuntu-drivers devices
```

![img1](https://github.com/TKTim/NVidia-2080Ti-Cuda10.2-Cudnn8.0-Yolo-GPU-/blob/master/Screenshot%20from%202020-06-16%2022-54-27.png)

有出現後，代表沒甚麼問題。

```
# ubuntu-drivers autoinstall
```
安裝成功！！！

下載CUDA-toolkit=CUDA
=

透過 #nvidia-smi 查看GPU狀況：

![img2](https://github.com/TKTim/NVidia-2080Ti-Cuda10.2-Cudnn8.0-Yolo-GPU-/blob/master/Screenshot%20from%202020-06-16%2022-56-48.png)

右上角有清楚告訴你該下載的CUDA版本，我的是10.2
所以 [GOGO](https://developer.nvidia.com/cuda-toolkit-archive)， 找到自己的版本下載下來吧。
像我的就長這樣：

![img3](https://github.com/TKTim/NVidia-2080Ti-Cuda10.2-Cudnn8.0-Yolo-GPU-/blob/master/Screenshot%20from%202020-06-16%2022-59-42.png)

那就照著官網，把程式碼打一打吧！

再運作的時候，有可能會出現

<font style="color:red"> │ Existing package manager installation of the driver found. It is strongly    ││ recommended that you remove this before continuing. </font>

這時候毫不猶豫的給他Continue下去，接下來很重要

### 接下來很重要

### 接下來很重要

### 接下來很重要

在他確認你要安裝哪些檔案時，請把driver取消勾選。因為我們下載過了！！！

# 到你的 ~/.bashrc 最下面，增加這兩行，檔案跟我不一樣就換掉就好。

```
export PATH="$PATH:/usr/local/cuda-10.2/bin"
export LD_LIBRARY_PATH="/usr/local/cuda-10.2/lib64:$LD_LIBRARY_PATH"
```

### 重開之後，輸入
```
nvcc -V
```
會看到：

![img4](https://github.com/TKTim/NVidia-2080Ti-Cuda10.2-Cudnn8.0-Yolo-GPU-/blob/master/Screenshot%20from%202020-06-16%2023-11-34.png)

就代表你成功安裝了

下載Cudnn
=
[Come on Baby](https://developer.nvidia.com/rdp/cudnn-download)
我是選擇下載Runtime檔案
下載後
```
# cd 到下載目錄
# dpkg -i <檔案名稱>
像我的是：
dpkg -i libcudnn8_8.0.0.180-1+cuda10.2_amd64.deb 
```

這樣一切就好了
記得重新開機。

下載YOLO
=
```
git clone https://github.com/pjreddie/darknet
cd darknet
make
```
就這麼簡單，再來
```
wget https://pjreddie.com/media/files/yolov3.weights
下載預先的權重檔
```
測試看看
```
./darknet detect cfg/yolov3.cfg yolov3.weights data/dog.jpg
```
![im](https://github.com/TKTim/NVidia-2080Ti-Cuda10.2-Cudnn8.0-Yolo-GPU-/blob/master/Screenshot%20from%202020-06-18%2020-30-03.png)
![im](https://github.com/TKTim/NVidia-2080Ti-Cuda10.2-Cudnn8.0-Yolo-GPU-/blob/master/Screenshot%20from%202020-06-18%2020-30-12.png)

### 之後再到 predictions.png 看看你的成果，那麼以上
### 都是沒有GPU，也沒有OpenCV的，就下來就來教各位吧！

下載Opencv
=

基本上
```
sudo apt-get install libopencv-dev python-opencv
```
就夠了，下載後運行
```
pkg-config --modversion opencv
察看OpenCV的版本。
```
如果不行，就請看看[這裡](https://wenyuangg.github.io/posts/opencv/opencv-installation.html)

結束後，就來大組裝

架設最終YOLO
=

```
# cd /darknet
#vim Makefile
```
#### 將GPU和OPENCV都 =1
![im](https://github.com/TKTim/NVidia-2080Ti-Cuda10.2-Cudnn8.0-Yolo-GPU-/blob/master/Screenshot%20from%202020-06-18%2020-33-59.png)






