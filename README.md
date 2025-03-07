[toc]

# English version

I am writing a simplified English version (about half size of the Chinese version) of the book:

* [Chapter 1 (**finished**)](https://github.com/brucefan1983/CUDA-Programming/blob/master/src/01-introduction/readme.md)
* [Chapter 2 (**finished**)](https://github.com/brucefan1983/CUDA-Programming/blob/master/src/02-thread-organization/readme.md)
* [Chapter 3 (**finished**)](https://github.com/brucefan1983/CUDA-Programming/blob/master/src/03-basic-framework/readme.md)
* [Chapter 4 (**finished**)](https://github.com/brucefan1983/CUDA-Programming/tree/master/src/04-error-check)
* [Chapter 5 (**finished**)](https://github.com/brucefan1983/CUDA-Programming/tree/master/src/05-prerequisites-for-speedup)

# 友情链接
* 由琪同学正在用 pyCUDA 实现本书中的范例，见如下仓库（似乎已停止更新）：
https://github.com/YouQixiaowu/CUDA-Programming-with-Python

# 关于本书第一版：

## 封面

注意：本书仅有 184 页，没有如下封面展示的那么厚。该封面只是编辑发给我的一个示意图，而不是实物图。要点：不要对本书的厚度（及深度）有太高的期望，否则会有点失望。

![cover](cover.jpg)

## 购买渠道

已于2020年10月由清华大学出版社出版，语言为中文。在京东或者淘宝搜索“CUDA 编程 樊哲勇”可找到本书。

## 第一版勘误

本仓库的 master 分支将对应开发版本，与第一版对应的源代码见此[发布版本](https://github.com/brucefan1983/CUDA-Programming/releases/tag/v1.0)。欢迎读者针对本书找错。找到一个其他人没有报告的错误并说服我改正者，我承诺送您此书第二版一本。目前收到的错误报告如下：

| 报告者       | 错误类型 | 页码信息  |  更正信息 |
|:------------|:---------------|:---------------|:---------------|
| GPUSLady | 笔误 | 前言 | “苏州吉浦**讯**科技有限公司”应改为“苏州吉浦**迅**科技有限公司”。 |
| EverNorif | 笔误 | 第 34 页 | “调用该核函时” 应改为 “调用该核函数时”。 | 
| Ebrece | 笔误 | 第 52-53 页 | `$ nvcc -O3 -arch=sm_75 -arithmetic1cpu.cu` 应改为 `$ nvcc -O3 -arch=sm_75 arithmetic1cpu.cu`。类似地，`$ nvcc -O3 -arch=sm_75 -arithmetic2gpu.cu` 应改为 `$ nvcc -O3 -arch=sm_75 arithmetic2gpu.cu`。 | 
| Ebrece | 笔误 | 第 135 页 | 倒数第二行的“函数将退化同步的”应改为“函数将退化**为**同步的”。|
| 我自己 | 不安全的代码 | 第 143 页 | 程序中第 23 行核函数的第二个参数 `size` 应改为 `size / sizeof(uint64_t)`。我已修改本仓库中 [对应的程序](https://github.com/brucefan1983/CUDA-Programming/blob/master/src/12-unified-memory/oversubscription2.cu)。 |
| 某网友 | 笔误 | 第 106 页 | “在10.1节”应改为“在第10.2节”。|
| 静听风吟 | 认知错误 | 第 3 页 |  表 1.2 中，Jetson 系列的显卡没有图灵架构的，应把 “AGX Xavier” 改成 “无”。|
| 静听风吟 | 认知错误 | 第 12 章 |  本章中关于统一内存的使用，错误地认为在使用第二代统一内存（在 Linux 系统中使用帕斯卡及以上架构的 GPU）的情况下，在调用核函数之后不需要进行主机与设备的同步即可 1）从主机访问任何统一内存数据；2）并总是得到正确的结果。以上论断中，1）是正确的，而 2）不正确，因为无论是使用第一代统一内存，还是使用第二代统一内存，在从主机访问被核函数修改的统一内存数据之前，都需要某种（显式的或隐式的）同步操作，才能避免读写竞争，从而保证结果的正确性。|
| Zhenkun Li | 错误的初始化 | 第 10 章 |  第 108 页尾部，语句 `real v = 0;` 应改为 `real v = s_y[tid];` |
| https://github.com/yuchangminghit | 错误的初始化 | 第 9 章 |  `neighbor2gpu.cu` 中，在调用核函数`find_neighbor_atomic`之前应该将数组 `d_NN` 的每个元素初始化为零，并去掉核函数中的初始化语句 `d_NN[n1] = 0;`|
| https://github.com/yuchangminghit | 错误的论述 | 第 10 章 | 第10.2节最后一段，从“如果想要在循环内去掉对线程号的约束”开始的论述是错误的，因为此处给的示范代码会导致非法显存访问。|


# 目录和源代码条目

## 第 1 章：GPU 硬件和 CUDA 工具

本章无源代码。

## 第 2 章：`CUDA` 中的线程组织

| 文件       | 知识点 |
|:------------|:---------------|
| `hello.cpp` | 用 `C++` 写一个 Hello World 程序 |
| `hello1.cu` | 一个正确的 `C++` 程序也是一个正确的 `CUDA` 程序 |
| `hello2.cu` | 写一个打印字符串的 `CUDA` 核函数并调用 |
| `hello3.cu` | 使用含有多个线程的线程块 |
| `hello4.cu` | 使用多个线程块 |
| `hello5.cu` | 使用两维线程块 |

## 第 3 章：`CUDA` 程序的基本框架

| 文件        | 知识点 |
|:------------|:---------------|
| `add.cpp`      | 数组相加的 `C++` 版本 |
| `add1.cu`      | 数组相加的 `CUDA` 版本 |
| `add2wrong.cu` | 如果数据传输方向搞错了会怎样？ |
| `add3if.cu`    | 什么时候必须在核函数使用 if 语句？ |
| `add4device.cu`| 定义与使用 `__device__` 函数 |

## 第 4 章：`CUDA` 程序的错误检测

| 文件       | 知识点 |
|:------------|:---------------|
| `check1api.cu`    | 检测 `CUDA` 运行时 API 函数的调用 |
| `check2kernel.cu` | 检测 `CUDA` 核函数的调用 |
| `memcheck.cu`     | 用 `cuda-memcheck` 检测内存方面的错误 |
| `error.cuh`       | 本书常用的用于检测错误的宏函数 |

## 第 5 章：获得 GPU 加速的前提

| 文件       | 知识点 |
|:------------|:---------------|
| `add1cpu.cu`    | 为 `C++` 版的数组相加函数计时 |
| `add2gpu.cu`    | 为数组相加核函数计时 |
| `add3memcpy.cu` | 如果把数据传输的时间也包含进来，还有加速吗？|
| `arithmetic1cpu.cu`       | 提高算术强度的 `C++` 函数 |
| `arithmetic2gpu.cu`       | 提高算术强度的核函数；GPU/CPU 加速比是不是很高？ |

## 第 6 章： `CUDA` 中的内存组织

| 文件        | 知识点 |
|:------------|:---------------|
| `static.cu`    | 如何使用静态全局内存 |
| `query.cu`     | 如何在 CUDA 程序中查询所用 GPU 的相关技术指标 |

## 第 7 章：全局内存的合理使用

| 文件        | 知识点 |
|:------------|:---------------|
| `matrix.cu` | 合并与非合并读、写对程序性能的影响 |

## 第 8 章：共享内存的合理使用

| 文件        | 知识点 |
|:------------|:---------------|
| `reduce1cpu.cu`     | `C++` 版本的归约函数 |
| `reduce2gpu.cu`     | 仅使用全局内存和同时使用全局内存和共享内存的归约核函数|
| `bank.cu`           | 使用共享内存实现矩阵转置并避免共享内存的 bank 冲突 |

## 第 9 章：原子函数的合理使用

| 文件        | 知识点 |
|:------------|:---------------|
| `reduce.cu`        | 在归约核函数中使用原子函数 `atomicAdd` |
| `neighbor1cpu.cu`  | CPU 版本的邻居列表构建函数 |
| `neighbor2gpu.cu`  | GPU 版本的邻居列表构建函数，分使用和不使用原子函数的情况 |

## 第 10 章: 线程束内部函数
| 文件        | 知识点 |
|:------------|:---------------|
| `reduce.cu` | 线程束同步函数、线程束洗牌函数以及协作组的使用 |
| `reduce1parallelism.cu` | 提高线程利用率 |
| `reduce2static.cu` | 利用静态全局内存加速  |

## 第 11 章： `CUDA` 流
| 文件        | 知识点 |
|:------------|:---------------|
| `host-kernel.cu`     | 重叠主机与设备计算 |
| `kernel-kernel.cu`   | 重叠核函数之间的计算 |
| `kernel-transfer.cu` | 重叠核函数执行与数据传输 |

## 第 12 章：统一内存
| 文件       | 知识点 |
|:------------|:---------------|
| `add.cu` | 使用统一内存可以简化代码 |
| `oversubscription1.cu` | 统一内存在初始化时才被分配  |
| `oversubscription2.cu` | 用 GPU 先访问统一内存时可以超过显存的容量 |
| `oversubscription3.cu` | 用 CPU 先访问统一内存时不可超过主机内存容量 |
| `prefetch.cu` | 使用 cudaMemPrefetchAsync 函数 |

## 第 13 章：分子动力学模拟（MD）
| 文件夹        | 知识点 |
|:------------|:---------------|
| `cpp`     | C++ 版本的 MD 程序 |
| `force-only`   | 仅将求力的函数移植到 CUDA |
| `whole-code` | 全部移植到 CUDA |

## 第 14 章：CUDA 库
| 文件        | 知识点 |
|:------------|:---------------|
| `thrust_scan_vector.cu`  | 使用 `thrust` 中的设备矢量 |
| `thrust_scan_pointer.cu` | 使用 `thrust` 中的设备指针 |
| `cublas_gemm.cu`         | 用 `cuBLAS` 实现矩阵相乘 |
| `cusolver.cu`            | 用 `cuSolver` 求矩阵本征值 |
| `curand_host1.cu`        | 用 `cuRAND` 产生均匀分布的随机数 |
| `curand_host2.cu`        | 用 `cuRAND` 产生高斯分布的随机数 |

# 我的部分测试结果

## 我的测试系统

* Linux: 主机编译器用的 `g++`。
* Windows: 仅使用命令行解释器 `CMD`，主机编译器用 Visual Studio 中的 `cl`。在用 `nvcc` 编译 CUDA 程序时，可能需要添加 `-Xcompiler "/wd 4819"` 选项消除和 unicode 有关的警告。
* 全书代码可在 `CUDA` 9.0-10.2 （包含）之间的版本运行。

## 矢量相加 (第 5 章)

* 数组元素个数 = 1.0e8。
* CPU (我的笔记本) 函数的执行时间是 60 ms （单精度）和 120 ms （双精度）。
* GPU 执行时间见下表：

|  V100 (S) | V100 (D) | 2080ti (S) | 2080ti (D) | P100 (S) | P100 (D) | laptop-2070 (S) | laptop-2070 (D) | K40 (S) | K40 (D) |
|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|:---------|
| 1.5 ms | 3.0 ms |  2.1 ms |  4.3 ms | 2.2 ms |  4.3 ms | 3.3 ms | 6.8 ms | 6.5 ms | 13 ms |

* 如果包含 cudaMemcpy 所花时间，GeForce RTX 2070-laptop 用时 180 ms （单精度）和 360 ms （双精度），是 CPU 版本的三倍慢！

## 一个高算术强度的函数（第 5 章）
* CPU 函数（数组长度为 10^4）用时 320 ms （单精度）和 450 ms （双精度）。
* GPU 函数（数组长度为 10^6）用时情况如下表：

|  V100 (S) | V100 (D) | 2080ti (S) | 2080ti (D) | laptop-2070 (S) | laptop-2070 (D) |
|:---------|:---------|:---------|:---------|:---------|:---------|
| 11 ms | 28 ms |  15 ms |  450 ms | 28 ms |  1000 ms |

* 用 GeForce RTX 2070-laptop 时核函数执行时间与数组元素个数 N 的关系见下表（单精度）：

| N    | 时间 |
|:-------|:-------|
| 1000    | 0.91 ms |
| 10000   | 0.99 ms |
| 100000  | 3.8 ms |
| 1000000 | 28 ms |
| 10000000   | 250 ms |
| 100000000  | 2500 ms |

## 矩阵复制和转置 (第 7-8 章)
* 矩阵维度为 10000 乘 10000。
* 核函数执行时间见下表：

| 计算     | V100 (S) | V100 (D) | 2080ti (S) | 2080ti (D) | K40 (S) |
|:---------------------------------|:-------|:-------|:-------|:-------|:-------|
| 矩阵复制                             | 1.1 ms | 2.0 ms | 1.6 ms | 2.9 ms |  |
| 读取为合并、写入为非合并的矩阵转置     | 4.5 ms | 6.2 ms | 5.3 ms | 5.4 ms | 12 ms |
| 写入为合并、读取为非合并的矩阵转置     | 1.6 ms | 2.2 ms | 2.8 ms | 3.7 ms | 23 ms |
| 在上一个版本的基础上使用 `__ldg` 函数 | 1.6 ms | 2.2 ms | 2.8 ms | 3.7 ms | 8 ms |
| 利用共享内存转置，但有 bank 冲突      | 1.8 ms | 2.6 ms | 3.5 ms | 4.3 ms |  |
| 利用共享内存转置，且无 bank 冲突      | 1.4 ms | 2.5 ms | 2.3 ms | 4.2 ms |  |

## 数组归约（第 8-10 章）

* 数组长度为 1.0e8，每个元素为 1.23。
* 归约的精确结果为 123000000。
* GPU 为笔记本版本的 GeForce RTX 2070。
* 下面是用**单精度**浮点数测试的结果：

| 计算方法与机器                         | 计算时间 |   结果  |
|:----------------------------------------------|:----------|:----------|
| CPU 中循环累加                        | 100 ms | 33554432 （**完全错误**） |
| 全局内存+线程块同步函数                | 5.8 ms  | 123633392 （**三位**正确的有效数字）|
| 静态共享内存+线程块同步函数            | 5.8 ms | 123633392 （**三位**正确的有效数字）|
| 动态共享内存+线程块同步函数            | 5.8 ms | 123633392 （**三位**正确的有效数字）|
| 共享内存+原子函数+线程块同步函数        | 3.8 ms |123633392 （**三位**正确的有效数字）|
| 共享内存+原子函数+线程束同步函数        | 3.4 ms |123633392 （**三位**正确的有效数字）|
| 共享内存+原子函数+线程束洗牌函数        | 2.8 ms |123633392 （**三位**正确的有效数字）|
| 共享内存+原子函数+协作组               | 2.8 ms |123633392 （**三位**正确的有效数字）|
| 共享内存+协作组+两个核函数             | 2.0 ms |123000064 （**七位**正确的有效数字）|
| 共享内存+协作组+两个核函数+静态全局内存 | 1.5 ms |123000064 （**七位**正确的有效数字）|

## 邻居列表（第 9 章）

* 原子数为 22464。
* 使用单精度或双精度时，CPU 都用时约 250 毫秒。
* GPU 测试结果见下表：

| 是否使用原子函数     | V100 (S) | V100 (D) | RTX 2070 (S) | RTX 2070 (D) |
|:----------------|:---------|:---------|:-----------|:-----------|
| 否 | 1.9 ms | 2.6  ms | 2.8 ms | 23 ms |
| 是    | 1.8 ms | 2.6  ms | 2.5 ms | 16 ms |

## 分子动力学模拟（第 13 章）

* 模拟体系为固态氩
* GPU 为笔记本中的 RTX 2070，使用单精度浮点数
* CPU 为 Intel i7-8750H 处理器

### CPU 版本计算速度测试
* 原子数 N = 10^3 * 4 = 4000
* 产出步数 = 20000
* 各个部分所花时间见下表

| 求力部分     | 运动方程积分部分 | 全部 |
|:----------------|:---------|:-----------|
| 62 s| 0.7 s | 62.7 s |

### force-only 版本的计算速度测试

| 原子数  | 产出步数   | 求力和数据传输的时间 | 运动方程积分的时间  | 全部时间 | 整体速度|
|:----------------|:---------|:-----------|:-----------|:-----------|:-----------|
| 4000 | 20000 | 5.8 s | 0.7 s  |  6.5 s  | 1.2e7 原子步每秒|
| 32000 | 10000 | 5.0 s | 2.5 s  |  7.5 s  | 4.3e7 原子步每秒|
| 108000 | 4000 | 5.4 s | 3.3 s  |  8.7 s  | 5.0e7 原子步每秒|
| 256000 | 2000 | 5.4 s | 4.6 s  |  10 s  | 5.1e7 原子步每秒|

### whole-code 版本的计算速度测试

| 原子数  | 产出步数   | 求力的时间 | 运动方程积分的时间 | 全部时间 | 整体速度|
|:----------------|:---------|:-----------|:----------|:-----------|:-----------|
| 4000 | 20000 | 1.5 s | 0.6 s  |  2.1 s  | 3.8e7 原子步每秒|
| 32000 | 10000 | 1.6 s | 0.3 s  |  1.9 s  | 1.7e8 原子步每秒|
| 108000 | 4000 | 2.0 s | 0.4 s  |  2.4 s  | 1.8e8 原子步每秒|
| 256000 | 2000 | 2.2 s | 0.4 s  |  2.6 s  | 2.0e8 原子步每秒|
