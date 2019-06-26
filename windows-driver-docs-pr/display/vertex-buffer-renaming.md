---
title: 顶点缓冲区重命名
description: 顶点缓冲区重命名
ms.assetid: b76552b4-77a9-43f4-984b-10de92dffa83
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，请重命名的顶点缓冲区
- 顶点缓冲区 DirectX WDK 8.0，重命名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4a72ecc783372824f0d7931c3248478a13e2097
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385562"
---
# <a name="vertex-buffer-renaming"></a>顶点缓冲区重命名


## <span id="ddk_vertex_buffer_renaming_gg"></span><span id="DDK_VERTEX_BUFFER_RENAMING_GG"></span>


若要提高该驱动程序和运行时之间的并行度，Direct3D 支持顶点缓冲区"重命名"的概念。 实际上，这是用于顶点缓冲区的双缓冲方案。 在某些情况下，驱动程序可以传递通过 DDI 调用的顶点缓冲区时，将修改顶点缓冲区的视频内存的指针。 这种方式，该驱动程序可以继续处理顶点缓冲区的内容，而在相同时，应用程序可以锁定并填充顶点缓冲区。 就应用程序而言，它使用相同的顶点缓冲区。 指向由该顶点缓冲区的内存已修改的事实是隐藏的运行时和驱动程序。

尽管早期版本的 DirectX 支持顶点缓冲区重命名有已使用 DirectX 8.0 某些更改。 在以前版本的 Direct3D，重命名主要完成通过[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI 入口点。 中指定的标志[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)是否驱动程序可以交换的顶点和命令缓冲区，以及如果出现这种情况，将指定的缓冲区所需的大小将是。 但是，在 DirectX 8.0 中，顶点缓冲区交换不通过实现*D3dDrawPrimitives2* （尽管通过旧接口的调用仍利用此机制） 而通过*LockExecuteBuffer* ([*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))) DDI 入口点。

DirectX 8.0 定义新的锁标志 D3DLOCK\_放弃，，当传递给驱动程序时，指示调用方不需要的驱动程序的现有内容，它们可以返回到顶点缓冲区数据的指针之前忽略的因此。 因此，当驱动程序收到的顶点缓冲区锁调用与 D3DLOCK\_放弃标志设置，它可以选择重命名的顶点缓冲区通过设置**fpVidMem**为新值。

请注意，D3DLOCK\_初始零售版本的 Windows 2000 不向驱动程序传递放弃标志。 该标志将在 Windows 2000 Service Pack 1 (SP1) 和所有后续版本的 Windows 2000 上传递。

在 DirectX 7.0 中，顶点缓冲区重命名也可通过*LockExecuteBuffer*使用标志 DDLOCK\_DISCARDCONTENTS。 但是，运行时和 DirectX 7.0 的原始发行版上的驱动程序之间的同步会阻止此机制无法正常工作。 但是，与 DirectX 8.0 一起发行的 DirectX 7.0 的版本纠正此问题和顶点缓冲区重命名在锁定时是否通过 DirectX 7.0 接口正常运行。

 

 





