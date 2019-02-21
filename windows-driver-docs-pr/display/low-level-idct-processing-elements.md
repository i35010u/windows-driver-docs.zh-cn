---
title: 低级别 IDCT 处理元素
description: 低级别 IDCT 处理元素
ms.assetid: 7736a226-1122-4380-b09f-a8560c0cd609
keywords:
- 宏块 WDK DirectX va，因此 IDCT
- 低级别 IDCT WDK DirectX VA
- 关闭主机 IDCT WDK DirectX VA
- 基于主机的 IDCT WDK DirectX VA
- 逆变离散余弦 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e8d30d07de56ac537e0e7a28f1fc2786b5c655
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526638"
---
# <a name="low-level-idct-processing-elements"></a>低级别 IDCT 处理元素


## <span id="ddk_low_level_idct_processing_elements_gg"></span><span id="DDK_LOW_LEVEL_IDCT_PROCESSING_ELEMENTS_GG"></span>


DirectX VA 接口支持处理低级别的反余弦值离散转换的各种方法 (*IDCT*)。 有两种基本类型的操作：

1.  关闭主机 IDCT:传递到外部 IDCT、 图片重建和重新构造剪辑的加速器转换系数的块效应。

2.  基于主机的 IDCT:有关空间域结果给快捷键用于外部图片重建和重新构造剪辑主机并传递块执行 IDCT。

在这两种情况下，主机上执行基本的逆量化进程、 预 IDCT 范围饱和度、 MPEG 2 不匹配控件 （如有必要） 和内部 DC 偏移量 （如果有必要）。 在这两种情况下，快捷键完成最终图片重建和重新构造剪辑。

反量化、 预 IDCT 饱和度、 不匹配控件、 内部 DC 偏移量、 IDCT、 图片重建和重新构造剪辑进程的以下步骤中定义。 [ **DXVA\_QmatrixData** ](https://msdn.microsoft.com/library/windows/hardware/ff564034)结构加载逆量化矩阵数据压缩视频图片解码。 (的值*BPP*， *W*<sub>T</sub>，以及*H*<sub>T</sub>应假定为等于 8，除非否则为通过指定[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构。)

1. 创建 IDCT 系数值的一组执行 （包括应用程序的任何反量化权重矩阵） 根据反量化*F"(u,v)* 从平均信息量编码量化索引处开始。 由主机执行此操作。

2. 使每个重新构造的系数值饱和*F"(u,v)* 用于获取一个值的转换系数块*F'(u,v)* 下面的公式中定义受限制的允许范围内。 由主机执行此操作。![说明预反离散的余弦值的计算转换 (pre idct) 饱和度](images/formula1.png)

3. MPEG 2 执行不匹配控件。 （此阶段的处理需要 MPEG 2 仅。）不匹配控件执行的所有其他系数宏块中的饱和的值求和 (这相当于 XORing 其最低有效位)。 如果总和为偶数，从最后一个系数的饱和值中减去 1 *F'*(*W*<sub>T</sub>*-1，H*<sub>T</sub>*为-1*)。 如果总和为奇数，饱和的值*F (W*<sub>T</sub>*-1，H*<sub>T</sub><em>为-1)</em> * <strong><em>按原样使用，无需更改。饱和度和不匹配的控件之后创建的系数值称为 *F(u,v)</em>本文档中。由主机执行此操作。* * 请注意</strong>mpeg-1 具有不匹配控件更改值相差正或负 1 表示其他可能需要另外一个偶数值反量化后每个系数组成的一个不同的窗体。 H.263 不需要在本部分中所述的不匹配控件。 在任何情况下，不匹配控件是主机的责任，如果需要。

     

4. 添加内部 DC 偏移量 （如果有必要） 对所有内部块因此所有内部块都表示相对于 2 的空间引用预测值的差异<sup>(BPP-1)</sup>。 此类偏移量是必需的所有引用视频编码标准 （H.261、 H.263、 mpeg-1、 MPEG 2 和 MPEG 4） 时除外*HostResidDiff*为 1 并**bConfigIntraResidUnsigned**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构为 1。 内部 DC 偏移量的值 (2<sup>(BPP-1)</sup>) \* sqrt (*W*<sub>T</sub>*H*<sub>T</sub>) 中转换域。 此值是在所有情况下，除 MPEG-4，允许 1024年*BPP*大于 8。 由主机执行此操作。

5. 主机或加速器上执行离散的反余弦值转换 (IDCT)。 IDCT 指定由以下公式，其中：*C*(*u*) = 1，为*u* = 0，否则*C(u)* = sqrt(2) *C*(*v*) = 1，为*v* = 0，否则*c （v)* = sqrt(2) *x*并*y*是像素域中的水平和垂直空间坐标*u*并*v*是转换域水平和垂直频率坐标*W*<sub>T</sub>和*H*<sub>T</sub>是宽度和高度 （通常两者都是 8） 的转换块。
6. 添加到的空间域残留信息[经过运动补偿预测](motion-compensated-prediction.md)nonintra 块或内部块加速器上执行图片重新构造的常量引用值的值。 内部块的常量引用值为 2<sup>(BPP-1)</sup>例外 HostResidDiff (位的 10 **wMBtype**的成员[ **DXVA\_MBctrl\_P\_HostResidDiff\_1**](https://msdn.microsoft.com/library/windows/hardware/ff563993)) 结构为 1 并**bConfigIntraResidUnsigned**隶属[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构为 1。 在后一种情况下，该常数为零。

7. 剪裁图片重建到一个范围从 0 到 (2<sup>BPP</sup>)-1 和存储最终得到的图片示例加速器上的值。

 

 





