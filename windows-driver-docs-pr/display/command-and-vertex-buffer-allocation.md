---
title: 命令和顶点缓冲区分配
description: 命令和顶点缓冲区分配
ms.assetid: 07666a6f-1d2e-4f30-bba8-a09b59225ecf
keywords:
- 命令缓冲区 WDK Direct3D
- 顶点缓冲区 WDK Direct3D
- WDK Direct3D 缓冲区
- 分配 Direct3D 缓冲区
- 隐式顶点缓冲区 WDK Direct3D
- 显式顶点缓冲区 WDK Direct3D
- DDSCAPS2_VERTEXBUFFER
- DDSCAPS2_COMMANDBUFFER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55e87aceba35e03e1d90a71a0089ad5314157b21
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370688"
---
# <a name="command-and-vertex-buffer-allocation"></a>命令和顶点缓冲区分配


## <span id="ddk_command_and_vertex_buffer_allocation_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFER_ALLOCATION_GG"></span>


有三种类型在 Direct3D 中使用的缓冲区大小：

-   创建仅; 供内部使用的隐式顶点缓冲区也就是说，应用程序不知道它们。 上下文创建后始终创建一个隐式顶点缓冲区和 Direct3D 将顶点数据存储在它们。

-   显式顶点缓冲区，只能在应用程序请求的响应中创建。 然后，Direct3D 显式顶点缓冲区中存储顶点数据。

-   命令缓冲区，供内部使用; 仅创建也就是说，应用程序不知道的命令缓冲区。 Direct3D 命令缓冲区中存储命令数据。

隐式顶点缓冲区是由 Direct3D 在内部使用进行批处理的特殊顶点缓冲区。 它们在设备初始化期间创建，并可在 multibuffered。 它们是始终读/写使它们不应将放在视频内存中 （适用于 Microsoft DirectX 6.0 和更高版本）。 此类型的缓冲区标记由这两个 DDSCAPS2 缺少\_VERTEXBUFFER 和 DDSCAPS2\_COMMANDBUFFER 标志。

创建和控制的应用程序显式顶点缓冲区。 这些不能为 multibuffered 和能将其放到本地或非本地的视频内存，除非 DDSCAPS\_WRITEONLY 标志设置。 显式顶点缓冲区都标有 DDSCAPS\_VERTEXBUFFER。

命令缓冲区 Direct3D 使用批处理命令。 它们可以是 multibuffered 并且用于除 TLVERTEX 或未剪辑执行缓冲区 API 调用之外的所有 Api。 此类型的缓冲区标记由标志 DDSCAPS2\_COMMANDBUFFER。 它们始终是只写的但没有显式标记设置，它们永远不会包含无效的指令。

默认情况下，Direct3D 运行时分配所有这类缓冲区。 通过与它们相关联的图面来访问隐式顶点缓冲区和命令缓冲区。 传递给驱动程序的所有缓冲区[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调。

### <a name="span-iddriver-allocatedvertexandcommandbuffersspanspan-iddriver-allocatedvertexandcommandbuffersspanspan-iddriver-allocatedvertexandcommandbuffersspandriver-allocated-vertex-and-command-buffers"></a><span id="Driver-Allocated_Vertex_and_Command_Buffers"></span><span id="driver-allocated_vertex_and_command_buffers"></span><span id="DRIVER-ALLOCATED_VERTEX_AND_COMMAND_BUFFERS"></span>驱动程序分配的顶点和命令缓冲区

Direct3D 驱动程序 （可选） 通过提供回调函数来执行顶点和命令缓冲区的分配。 若要提供这些回调函数，Direct3D 驱动程序填写[ **DD\_D3DBUFCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_d3dbufcallbacks)结构和点**lpD3DBufCallbacks**的成员[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)到它的结构。 DD\_返回 HALINFO [ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)响应 DirectDraw 组件的驱动程序的初始化。 DD 中报告回调\_D3DBUFCALLBACKS 结构是：

-   [*CanCreateD3DBuffer*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_cancreatesurface)

-   [*CreateD3DBuffer*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurface)

-   [*DestroyD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

这些函数调用的方式相同*DdXxxSurface*回调 (例如[ *DdCanCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))) 和仅当 DDSCAPS\_EXECUTEBUFFER设置标志。 缓冲区创建标志是 DDSCAPS\_WRITEONLY、 DDSCAPS2\_VERTEXBUFFER 和 DDSCAPS2\_COMMANDBUFFER。

驱动程序确定的类型通过检查所请求的缓冲区**ddsCaps**的成员[ **DD\_图面\_本地**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)结构传递给**CanCreateExecuteBuffer**并**CreateExecuteBuffer**回调的以下标志：

-   DDSCAPS\_VERTEXBUFFER 指示驱动程序应分配显式顶点缓冲区。

-   DDSCAPS\_COMMANDBUFFER 指示驱动程序应分配命令缓冲区。

-   如果设置了任一标志，该驱动程序应分配的隐式顶点缓冲区。

该驱动程序在内部分配顶点和命令缓冲区并循环显示这些缓冲区。 Direct3D 填充给定的对同时从其他排队缓冲区以异步方式呈现硬件。 这是使用直接内存访问 (DMA) 非常有用。

缓冲区 multibuffering 集中可能在不同的内存类型中，也就是说，在系统或视频内存中。 当调用该驱动程序时创建第一个缓冲区时，它立即会创建一组和到 Direct3D，返回集合中第一个缓冲区。 该驱动程序使用标志来指定使用它来集中每个缓冲区分配的内存的类型。 该驱动程序应在每次调用的系统内存中返回一个新的缓冲区[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)如果 D3DHALDP2\_SWAPVERTEXBUFFER 或 D3DHALDP2\_SWAPCOMMANDBUFFER 标志设置。 如果返回的缓冲区是在视频内存中，相应 D3DHALDP2\_VIDMEMVERTEXBUF 或 D3DHALDP2\_VIDMEMCOMMANDBUF 标志应设置。

有时，Direct3D 请求下一个缓冲区的最小大小。 如果大小太大，驱动程序应分配在系统内存 （后备面） 中的缓冲区。 如果大小太小，该驱动程序允许提供更大的缓冲区。 该驱动程序应跟踪的多少缓冲，哪些内存而清理退出上的所有内容的类型。

 

 





