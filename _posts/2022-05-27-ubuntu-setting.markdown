---
layout: post
title: "우분투 20.04 CUDA11.2 cuDNN8.1.0"
date: 2022-05-27 08:32:20 +0900
description: ubuntu 20.04 nvidia driver, CUDA, cuDNN initial setting
img:  # Add image post (optional)
categories: [Ubuntu]
---

## 우분투 20.04 CUDA11.2 cuDNN8.1 설치 커맨드 모음

  
1. nvidia driver 설치
```console
    $ ubuntu-drivers devices
    $ sudo apt install nvidia-driver-450
    $ sudo apt install nvidia-utils-450  
    $ sudo apt-get install build-essential
    $ nvidia-smi
```
- Titan XP 기준
- nvidia-smi 전에 한번 컴퓨터 껐다 켜야함. 그 김에 언어 설정 가능하게 iBUS 업데이트 하는 것 추천  
  
2. CUDA 설치
```console
    $ wget https://developer.download.nvidia.com/compute/cuda/11.2.2/local_installers/cuda_11.2.2_460.32.03_linux.run
    $ sudo sh cuda_11.2.2_460.32.03_linux.run
    $ sudo sh -c "echo 'export PATH=$PATH:/usr/local/cuda-11.2/bin' >> /etc/profile"
    $ sudo sh -c "echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.2/lib64' >> /etc/profile"
    $ sudo sh -c "echo 'export CUDADIR=/usr/local/cuda-11.2' >> /etc/profile"
    $ source /etc/profile
    $ nvcc -V
```  

3. cuDNN 설치(nvidia driver에서 cudnn 버전 맞는 파일 다운로드 [cuDNN Archive][cudnn-archive] )
```console
    $ cd Downloads/
    $ tar xvzf cudnn-11.2-linux-x64-v8.1.0.77.tgz 
    $ sudo cp cuda/include/cudnn* /usr/local/cuda/include
    $ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
    $ sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_train.so.8.1.0 /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_train.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8.1.0 /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_infer.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_train.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_adv_infer.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8.1.0  /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_ops_train.so.8
    $ sudo ln -sf /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8.1.0 /usr/local/cuda-11.2/targets/x86_64-linux/lib/libcudnn_cnn_infer.so.8
    $ sudo ldconfig
    $ cd
    $ ldconfig -N -v $(sed 's/:/ /' <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn
```
   
 4. 파이썬이 python 3.8 바라보게 하기
```console
    $ sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.8 1
    $ python --version
```
  
 5. 하드디스크 부팅시 자동마운트
```console
    $ sudo gedit /etc/fstab
```
  
 6. 파이참, itksnap 다운로드
```console
    $ sudo snap install pycharm-community --classic
    $ sudo apt-get install itksnap
```
    
    첫번째 포스팅 끝 ㅎㅅㅎ


[cudnn-archive]: https://developer.nvidia.com/rdp/cudnn-archive
