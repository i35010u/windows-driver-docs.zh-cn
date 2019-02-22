---
title: 边缘筛选命令字节
description: 边缘筛选命令字节
ms.assetid: eefb580a-133d-4c9e-a8d2-2d114107e2ea
keywords:
- 宏块 WDK DirectX VA，消除马赛克功能筛选器控件
- 消除筛选器控件 WDK DirectX VA 马赛克功能
- 边缘筛选 WDK DirectX VA
- 读回缓冲区 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 933880b385a3bf0098e0d90ea6d64a025b926ea4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545308"
---
# <a name="edge-filtering-command-bytes"></a>边缘筛选命令字节


## <span id="ddk_edge_filtering_command_bytes_gg"></span><span id="DDK_EDGE_FILTERING_COMMAND_BYTES_GG"></span>


每个边缘筛选控制命令包含一个字节。 *DXVA\_DeblockingEdgeControl*中定义常量*dxva.h*定义如何消除马赛克功能边缘进行处理。 7 的最高有效位的字节包含*EdgeFilterStrength*变量和最低有效位是*EdgeFilterOn*标志。

指定在 H.263 Annex J.作为执行边缘筛选*EdgeFilterStrength*变量指定的筛选要执行的强度。 *EdgeFilterOn*标志指定是否筛选为完成。 *EdgeFilterOn*如果边缘是筛选，并且如果不为零，则为 1。

边缘滤波 (与边缘*EdgeFilterOn*等于 1） 使用指定的强度值执行*EdgeFilterStrength*和剪辑到范围 0 到 2 的输出与<sup>(BPP)</sup> -1。 左边缘筛选任何块，因为用于顶部边缘筛选的示例的值必须是在之前的左边缘筛选任何 deblocking 筛选这些重新构造的值之前执行顶部边缘的所有块的都筛选。

如果**bPicDeblockConfined**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构指示该示例的宏块之外的值不受影响当前消除马赛克功能筛选器命令缓冲区， *EdgeFilterOn*标志是左侧和顶部的涵盖的使用消除马赛克功能在缓冲区中的筛选器命令块效应的区域的所有边缘的零。

### <a name="span-idread-backbuffersspanspan-idread-backbuffersspanspan-idread-backbuffersspanread-back-buffers"></a><span id="Read-Back_Buffers"></span><span id="read-back_buffers"></span><span id="READ-BACK_BUFFERS"></span>读回缓冲区

一个读回命令缓冲区传递给快捷键时**bPicReadbackRequests**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构为 1。 此缓冲区中的数据的命令的快捷键 （在消除马赛克功能条件，如果适用） 之后的结果的最终图片宏块数据返回给主机。 如果加密协议正在使用中，可能会响应快捷键以读回请求通过返回的错误的含义、 错误数据或加密的数据 （如可通过加密协议指定）。

传递给快捷键的读回命令缓冲区必须包含读回命令包含单个**wMBaddress**宏块宏块控制命令要读取的成员。 **WMBaddress**成员是 16 位值，该值指定当前宏块的宏块地址光栅扫描顺序。 光栅扫描顺序 (基于**wPicWidthInMBminus1**并**wPicHeightInMBminus1**的成员[ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构) 定义，如下所示：

-   零是左上方宏块的地址。

-   **wPicWidthInMBminus1**是右上方宏块的地址。

-   **wPicHeightInMBminus1** x (**wPicWidthInMBminus1**+ 1) 是左下方宏块的地址。

-   (**wPicHeightInMBminus1**+ 1) x (**wPicWidthInMBminus1**+ 1)-1 为右下宏块的地址。

如果*BPP*中指定的那样**bBPPminus1**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构是 8，宏块数据将以 8 位无符号值的形式返回 (因此，黑色是名义上 Y = 16，Cb = Cr = 128，和白色是名义上 Y = 235，Cb = Cr = 128)。 如果*BPP*大于 8、 16 位无符号值的形式返回的数据。

宏块数据是从加速器返回到主机上的副本的读回命令缓冲区本身下, 一步的 32 字节对齐边界后跟填充窗体。 然后，在读回命令缓冲区中的每个块为每个宏块中的每个块 64 示例窗体中发送的顺序返回亮度和色度数据的宏块数据值。

宏块的残留差异块返回指定中 MPEG 2 图 6-10，6-11，6 到 12 的顺序 (Y 宏块，块的光栅扫描顺序跟 4:2:0 块的 Cb，跟在 4:2:0 块的 Cr。如果在 4:2:2 或 4： 在 4、 4:4 采样操作： 2:0 块后面跟有 4:2:2 块 Cb，跟在 4:2:2 块的 Cr。如果在 4: 4、 4:4 采样操作： 2:2 块后面跟有 4:4:4 块 Cb，跟在 4:4:4 块的 Cr)。

 

 





