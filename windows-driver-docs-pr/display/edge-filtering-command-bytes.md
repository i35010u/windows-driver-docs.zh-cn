---
title: 边缘筛选命令字节
description: 边缘筛选命令字节
ms.assetid: eefb580a-133d-4c9e-a8d2-2d114107e2ea
keywords:
- macroblocks WDK DirectX VA，deblocking filter control
- deblocking 筛选器控件 WDK DirectX VA
- 边缘筛选 WDK DirectX VA
- 读回缓冲 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baa4fd3b1339be795952b4392ca6fa659742dee1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838959"
---
# <a name="edge-filtering-command-bytes"></a>边缘筛选命令字节


## <span id="ddk_edge_filtering_command_bytes_gg"></span><span id="DDK_EDGE_FILTERING_COMMAND_BYTES_GG"></span>


每个边缘筛选控制命令都包含一个字节。 *DXVA*中定义的*DXVA\_DeblockingEdgeControl*常量定义处理 deblocking 边缘的方式。 该字节的7个最高有效位包含*EdgeFilterStrength*变量，并且最小有效位是*EdgeFilterOn*标志。

按 .H 附录 J 中的指定执行边缘筛选。*EdgeFilterStrength*变量指定要执行的筛选的强度。 *EdgeFilterOn*标志指定是否要执行筛选。 如果要筛选边缘，则*EdgeFilterOn*的值为 1; 否则为0。

使用*EdgeFilterStrength*指定的强度值和将输出剪裁到0到 2<sup>（BPP）</sup> -1 范围内的值，以*EdgeFilterOn*等于1的边缘进行边缘筛选。 所有块的上边缘筛选是在对任何块进行左边缘筛选之前执行的，因为用于顶层边缘筛选的样本的值必须是在进行任何 deblocking 筛选之前用于进行左边缘筛选的那些重新构造的值。

如果[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的**bPicDeblockConfined**成员指示当前 deblocking 筛选器命令缓冲区之外的 macroblocks 的示例值不受影响，则*EdgeFilterOn*标志为对于缓冲区中 macroblocks 与 deblocking 筛选器命令所覆盖的区域的左侧和顶部的所有边缘，为零。

### <a name="span-idread-back_buffersspanspan-idread-back_buffersspanspan-idread-back_buffersspanread-back-buffers"></a><span id="Read-Back_Buffers"></span><span id="read-back_buffers"></span><span id="READ-BACK_BUFFERS"></span>回读缓冲区

当[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的**bPicReadbackRequests**成员为1时，一个回读命令缓冲区会传递到快捷键。 此缓冲区中的数据将命令加速器返回最终的最终图片宏块（如果适用）到主机的数据（如果适用）。 如果正在使用加密协议，此加速器可以通过返回错误数据、错误数据或加密的数据（可能由加密协议指定）来响应回读请求。

传递到加速器的回发命令缓冲区必须包含回发命令，该命令由宏块 control 命令的单个**wMBaddress**成员组成，以便宏块得以读取。 **WMBaddress**成员是一个16位值，该值指定当前宏块的宏块地址（以光栅扫描顺序表示）。 光栅扫描顺序（基于[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的**wPicWidthInMBminus1**和**wPicHeightInMBminus1**成员）定义如下：

-   零是左上角宏块的地址。

-   **wPicWidthInMBminus1**是右上宏块的地址。

-   **wPicHeightInMBminus1** x （**wPicWidthInMBminus1**+ 1）是左下宏块的地址。

-   （**wPicHeightInMBminus1**+ 1） x （**wPicWidthInMBminus1**+ 1）-1 是右下宏块的地址。

如果[**DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的**bBPPminus1**成员中指定的*BPP*为8，则以8位无符号值的形式返回宏块数据（因此，黑色为通常 Y = 16，Cb = Cr = 128，白色为通常Y = 235，Cb = Cr = 128）。 如果*BPP*大于8，则返回的数据格式为16位无符号值。

宏块数据以读回命令缓冲区本身副本的形式从加速器返回到宿主，后跟下一个32字节对齐边界。 然后，将按照每个宏块中每个块的每个块64样本的形式，返回在回读命令缓冲区中发送的宏块数据值。

宏块中的残差块按在 MPEG-2 图6-10、6-11 和6-12 中指定的顺序返回（宏块的 x 扫描顺序，后跟 Cb 的4:2:0 块，后跟的4:2:0 块）。如果在4:2:2 或4:4:4 采样操作中，4:2:0 块后跟 Cb 的4:2:2 块，然后是 Cr 的4:2:2 块。如果在4:4:4 采样操作中，4:2:2 块后跟 Cb 的4:4:4 块，然后是 Cr 的4:4:4 块）。

 

 





