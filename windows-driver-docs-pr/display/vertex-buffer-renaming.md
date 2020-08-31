---
title: 顶点缓冲区重命名
description: 顶点缓冲区重命名
ms.assetid: b76552b4-77a9-43f4-984b-10de92dffa83
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、顶点缓冲区、重命名
- 顶点缓冲 WDK DirectX 8.0，重命名
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a91a517a742b3d51918a51225451fe2218d0402
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067019"
---
# <a name="vertex-buffer-renaming"></a>顶点缓冲区重命名


## <span id="ddk_vertex_buffer_renaming_gg"></span><span id="DDK_VERTEX_BUFFER_RENAMING_GG"></span>


为了改进驱动程序与运行时之间的并行性，Direct3D 支持顶点缓冲区 "重命名" 的概念。 实质上，这是顶点缓冲区的双缓冲方案。 在某些情况下，驱动程序可以在通过 DDI 调用传递顶点缓冲区时修改顶点缓冲区的视频内存指针。 通过这种方式，驱动程序可以继续处理顶点缓冲区的内容，同时，应用程序可以锁定和填充顶点缓冲区。 与应用程序相关的是，使用相同的顶点缓冲区。 由该顶点缓冲区指向的内存已被修改，由运行时和驱动程序隐藏。

尽管早期版本的 DirectX 支持的顶点缓冲区重命名，但 DirectX 8.0 已进行了一些更改。 在以前版本的 Direct3D 中，重命名主要是通过 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI 入口点实现的。 在 [**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data) 中指定的标志将指定驱动程序是否可以交换顶点或命令缓冲区，如果是，则应指定缓冲区的大小。 但是，在 DirectX 8.0 中，无法通过 *D3dDrawPrimitives2* (完成顶点缓冲交换，不过，通过传统接口的调用仍然利用此机制) 而不是通过 *LockExecuteBuffer* ([*LockD3DBuffer*](/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))) DDI 入口点。

DirectX 8.0 定义了一个新的锁定标志，D3DLOCK \_ 放弃，在传递给驱动程序时，指示调用方不需要驱动程序的现有内容，因此可以在将指针返回到顶点缓冲区数据之前将其丢弃。 因此，当驱动程序接收到带有 D3DLOCK 放弃标志集的顶点缓冲区锁调用时 \_ ，它可以选择通过将 **fpVidMem** 设置为新值来重命名顶点缓冲区。

请注意，D3DLOCK \_ 放弃标志将不会通过 Windows 2000 的初始零售版本传递给驱动程序。 该标志将在 Windows 2000 Service Pack 1 (SP1) 以及所有后续版本的 Windows 2000 上传递。

在 DirectX 7.0 中，还可以通过 *LockExecuteBuffer* 使用标志 DDLOCK DISCARDCONTENTS 来完成顶点缓冲区重命名 \_ 。 但是，在 DirectX 7.0 的原始版本上运行时和驱动程序之间的同步会阻止此机制正常工作。 但是，使用 DirectX 8.0 发布的 DirectX 7.0 版本可以纠正此问题，并且锁定时的顶点缓冲区重命名功能通过 DirectX 7.0 接口运行。

 

