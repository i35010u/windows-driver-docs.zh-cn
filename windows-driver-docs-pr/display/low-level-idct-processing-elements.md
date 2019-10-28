---
title: 低级别 IDCT 处理元素
description: 低级别 IDCT 处理元素
ms.assetid: 7736a226-1122-4380-b09f-a8560c0cd609
keywords:
- macroblocks WDK DirectX VA，IDCT
- 低级别 IDCT WDK DirectX VA
- 脱离主机 IDCT WDK DirectX VA
- 基于主机的 IDCT WDK DirectX VA
- 逆离散-余弦转换 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e658c589fcfeb53e0f2cfef3f1ae38de88c40fd1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840595"
---
# <a name="low-level-idct-processing-elements"></a>低级别 IDCT 处理元素


## <span id="ddk_low_level_idct_processing_elements_gg"></span><span id="DDK_LOW_LEVEL_IDCT_PROCESSING_ELEMENTS_GG"></span>


DirectX VA 接口支持多种方法来处理低级别反离散-余弦转换（*IDCT*）。 有两种基本类型的操作：

1.  脱离主机 IDCT：将转换系数的 macroblocks 传递到外部 IDCT、图片重建和重建剪辑的快捷键。

2.  基于主机的 IDCT：在主机上执行 IDCT，并将空间域结果块传递到加速器，以便进行外部图片重构和重建。

在这两种情况下，基本的反量化处理、IDCT 范围饱和、MPEG-2 不匹配控制（如有必要）和 DC 内偏移（如有必要）将在主机上执行。 在这两种情况下，将在快捷键上完成最后的图片重建和重建。

在以下步骤中，将定义反量化、预 IDCT 的饱和度、不匹配控制、DC 偏移量、IDCT、图片重建和重建剪辑进程。 [**DXVA\_QmatrixData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_qmatrixdata)结构为压缩的视频照片解码加载反量化矩阵数据。 （ *BPP*、 *W*<sub>T</sub>和*H*<sub>t</sub>的值应假定等于8，除非[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构中指定了其他值。）

1. 根据需要执行反向量化（包括应用任何反量化权重矩阵），以从熵编码的量化指数创建一组 IDCT 系数值*F "（u，v）* 。 这由主机执行。

2. 使 "转换系数" 块的每个重建系数值*f "（u，v）* 在受限制的允许范围内获取值*f （u，v）* ，如以下公式所示。 这由主机执行。![计算，用于说明预逆离散余弦转换（预 idct）饱和度](images/formula1.png)

3. 对 MPEG-2 执行不匹配控制。 （仅 MPEG-2 需要此处理阶段。）不匹配控制是通过对宏块中所有系数的饱和值求和（这等效于 XORing 最小有效位）来执行的。 如果总计为偶数，则从最后一个系数*F*（*W*<sub>t</sub> *-1，H*<sub>t</sub> *-1*）的饱和值中减去1。 如果总和不是奇数，则按原样使用*F ' 的饱和值（W*<sub>T</sub> *-1，H*<sub>t</sub><em>-1）</em>* <strong><em>，而不进行任何更改。在饱和度和不匹配控制后创建的系数值在本文档中称为 * F （u，v）</em> 。这由主机执行。* * 请注意</strong>，mpeg-2 包含不同形式的不匹配控件，该控件包括对每个系数的值（在反向量化后会有偶数值）更改加上或减1。 H. 不需要此部分中所述的不匹配控制。 在任何情况下，不匹配控制是主机在需要时的责任。

     

4. 将 DC 内偏移量（如有必要）添加到所有内部块，以便所有内部块表示与空间引用预测值 2<sup>（BPP-1）</sup>相关的差异。 对于所有被引用的视频编码标准（261、.H、MPEG-2、mpeg-2 和 MPEG-2），这种偏移都是必需的，但当*HostResidDiff*为1和 DXVA\_的**bConfigIntraResidUnsigned**成员时除外： [**ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构为1。 在转换域中，站内偏移量的值（2<sup>（BPP-1）</sup>） \* Sqrt （*W*<sub>t</sub>*H*<sub>t</sub>）。 此值在除 MPEG-4 以外的所有情况下均为1024，这允许*BPP*大于8。 这由主机执行。

5. 在主机或快捷键上执行反离散余弦转换（IDCT）。 IDCT 由以下公式指定，其中： *c*（*u*） = 1 代表*u* = 0，否则， *c （u）* = sqrt （2） *c*（*v*） = 1 表示*v* = 0，否则*c （v）* = sqrt （2） *x*和*y*是水平的像素域*u*和*v*中的垂直空间坐标是转换域的水平和垂直频率坐标， *W*<sub>t</sub>和*H*<sub>t</sub>是转换块的宽度和高度（通常都是8个）。
6. 将空间域残留信息添加到 nonintra 块的[运动补偿预测](motion-compensated-prediction.md)值，或添加到用于在快捷键上执行图片重建的块内的常量引用值。 内部块的常数引用值为 2<sup>（BPP-1）</sup> ，除非 HostResidDiff （\_DXVA 的**WMBtype**成员的第10个[**MBctrl\_P\_HostResidDiff\_1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1)）结构为1，ConfigPictureDecode 结构的[**DXVA\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode) bConfigIntraResidUnsigned 成员是1。 在后一种情况下，常量为零。

7. 将图片重建剪切为介于0到（2<sup>BPP</sup>）-1 之间的范围，并在快捷键上存储最终生成的图片示例值。

 

 





