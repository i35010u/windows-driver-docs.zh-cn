---
title: 边缘筛选命令字节
description: 边缘筛选命令字节
keywords:
- macroblocks WDK DirectX VA，deblocking filter control
- deblocking 筛选器控件 WDK DirectX VA
- 边缘筛选 WDK DirectX VA
- 读回缓冲 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 08473bc918dba329976efefd48f506df54c898d8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816889"
---
# <a name="edge-filtering-command-bytes"></a>边缘筛选命令字节


## <span id="ddk_edge_filtering_command_bytes_gg"></span><span id="DDK_EDGE_FILTERING_COMMAND_BYTES_GG"></span>


每个边缘筛选控制命令都包含一个字节。 *DXVA* 中定义的 *DXVA \_ DeblockingEdgeControl* 常量定义处理 deblocking 边缘的方式。 该字节的7个最高有效位包含 *EdgeFilterStrength* 变量，并且最小有效位是 *EdgeFilterOn* 标志。

按 .H 附录 J 中的指定执行边缘筛选。 *EdgeFilterStrength* 变量指定要执行的筛选的强度。 *EdgeFilterOn* 标志指定是否要执行筛选。 如果要筛选边缘，则 *EdgeFilterOn* 的值为 1; 否则为0。

边缘筛选 (对于 *EdgeFilterOn* 等于 1) 的边缘，使用 *EdgeFilterStrength* 指定的强度值执行，并将输出剪裁到0到 2 <sup> (BPP)</sup> -1 范围内。 所有块的上边缘筛选是在对任何块进行左边缘筛选之前执行的，因为用于顶层边缘筛选的样本的值必须是在进行任何 deblocking 筛选之前用于进行左边缘筛选的那些重新构造的值。

如果 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicDeblockConfined** 成员指示当前 deblocking 筛选器命令缓冲区之外的 macroblocks 的采样值不受影响 *，则 EdgeFilterOn 标志为* 零，其中包含 macroblocks 的 deblocking 筛选器命令在缓冲区中的所有边缘。

### <a name="span-idread-back_buffersspanspan-idread-back_buffersspanspan-idread-back_buffersspanread-back-buffers"></a><span id="Read-Back_Buffers"></span><span id="read-back_buffers"></span><span id="READ-BACK_BUFFERS"></span>回读缓冲区

当 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicReadbackRequests** 成员为1时，一个回读命令缓冲区会传递到快捷键。 此缓冲区中的数据将命令加速器返回最终的结果， (宏块在 deblocking 之后（如果适用) 到主机）。 如果正在使用加密协议，则该加速器可能会通过返回错误指示、错误数据或加密的数据来响应回发请求，)  (。

传递到加速器的回发命令缓冲区必须包含回发命令，该命令由宏块 control 命令的单个 **wMBaddress** 成员组成，以便宏块得以读取。 **WMBaddress** 成员是一个16位值，该值指定当前宏块的宏块地址（以光栅扫描顺序表示）。 基于 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构) 的 **wPicWidthInMBminus1** 和 **wPicHeightInMBminus1** 成员 (的光栅扫描顺序定义如下：

-   零是左上角宏块的地址。

-   **wPicWidthInMBminus1** 是右上宏块的地址。

-   **wPicHeightInMBminus1** x (**wPicWidthInMBminus1**+ 1) 是左下宏块的地址。

-    (**wPicHeightInMBminus1**+ 1) x (**wPicWidthInMBminus1**+ 1) -1 是右下宏块的地址。

如果 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bBPPminus1** 成员中指定的 *BPP* 为8，则宏块数据以8位无符号值的形式返回 (因此，黑色 is 通常 Y = 16，Cb = Cr = 128，白色为通常 y = 235，Cb = Cr = 128) 。 如果 *BPP* 大于8，则返回的数据格式为16位无符号值。

宏块数据以读回命令缓冲区本身副本的形式从加速器返回到宿主，后跟下一个32字节对齐边界。 然后，将按照每个宏块中每个块的每个块64样本的形式，返回在回读命令缓冲区中发送的宏块数据值。

宏块中的残留差异块以 MPEG-2 x 6-10、6-11 和6-12 中指定的顺序返回。宏块的 Y 块 (光栅扫描顺序，后跟 Cb 的4:2:0 块，后面是 Cr 的4:2:0 块。如果在4:2:2 或4:4:4 采样操作中，4:2:0 块后跟 Cb 的4:2:2 块，然后是 Cr 的4:2:2 块。如果在4:4:4 采样操作中，4:2:2 块后跟 Cb 的4:4:4 块，然后是 Cr) 的4:4:4 块。

 

