---
title: 命令和顶点缓冲区分配
description: 命令和顶点缓冲区分配
ms.assetid: 07666a6f-1d2e-4f30-bba8-a09b59225ecf
keywords:
- 命令缓冲区 WDK Direct3D
- 顶点缓冲 WDK Direct3D
- 缓冲 WDK Direct3D
- 分配 Direct3D 缓冲区
- 隐式顶点缓冲 WDK Direct3D
- 显式顶点缓冲 WDK Direct3D
- DDSCAPS2_VERTEXBUFFER
- DDSCAPS2_COMMANDBUFFER
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fd78cb7061552d5fd2f5a959b5fdbe7c8592c19
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839806"
---
# <a name="command-and-vertex-buffer-allocation"></a>命令和顶点缓冲区分配


## <span id="ddk_command_and_vertex_buffer_allocation_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFER_ALLOCATION_GG"></span>


Direct3D 中使用三种类型的缓冲区：

-   仅供内部使用的隐式顶点缓冲区;也就是说，应用程序不能识别它们。 一个隐式顶点缓冲区始终在上下文创建后创建，而 Direct3D 将顶点数据存储在其中。

-   显式顶点缓冲区，只为响应应用程序请求而创建。 然后，Direct3D 会在显式顶点缓冲区中存储顶点数据。

-   仅供内部使用的命令缓冲区;也就是说，应用程序不知道命令缓冲区。 Direct3D 将命令数据存储在命令缓冲区中。

隐式顶点缓冲区是 Direct3D 用于批处理的特殊顶点缓冲区。 它们是在设备初始化期间创建的，并且可以是 multibuffered。 它们始终是可读/写的，因此不应将其放入视频内存（对于 Microsoft DirectX 6.0 和更高版本）。 这种类型的缓冲区标记为缺少 DDSCAPS2\_VERTEXBUFFER 和 DDSCAPS2\_COMMANDBUFFER 标志。

显式顶点缓冲区由应用程序创建和控制。 除非设置了 DDSCAPS\_WRITEONLY 标志，否则无法 multibuffered，并且无法将其放入本地或非本地视频内存。 显式顶点缓冲区用 DDSCAPS\_VERTEXBUFFER 标记。

Direct3D 用于批处理命令的命令缓冲区。 它们可以是 multibuffered，可用于除 TLVERTEX 或未剪辑执行缓冲区调用之外的所有 Api。 此类型的缓冲区由标记 DDSCAPS2\_COMMANDBUFFER 标记。 它们始终是只写的，但未设置显式标志并且它们从不包含无效的指令。

默认情况下，Direct3D 运行时分配所有这些缓冲区。 可以通过与它们关联的图面来访问隐式顶点缓冲区和命令缓冲区。 所有缓冲区都将传递给驱动程序的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调。

### <a name="span-iddriver-allocated_vertex_and_command_buffersspanspan-iddriver-allocated_vertex_and_command_buffersspanspan-iddriver-allocated_vertex_and_command_buffersspandriver-allocated-vertex-and-command-buffers"></a><span id="Driver-Allocated_Vertex_and_Command_Buffers"></span><span id="driver-allocated_vertex_and_command_buffers"></span><span id="DRIVER-ALLOCATED_VERTEX_AND_COMMAND_BUFFERS"></span>驱动程序分配的顶点和命令缓冲区

Direct3D 驱动程序可通过提供回调函数来选择执行顶点和命令缓冲区分配。 为了提供这些回调函数，Direct3D 驱动程序会填写[**dd\_D3DBUFCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_d3dbufcallbacks)结构，并将[**dd\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**lpD3DBufCallbacks**成员指向该结构。 DD\_HALINFO 由[**DrvGetDirectDrawInfo**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)返回，以响应驱动程序的 DirectDraw 组件的初始化。 DD\_D3DBUFCALLBACKS 结构中报告的回调如下：

-   [*CanCreateD3DBuffer*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_cancreatesurface)

-   [*CreateD3DBuffer*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurface)

-   [*DestroyD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

这些函数的调用方式与*DdXxxSurface*回调（如[*DdCanCreateSurface*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))）相同，并且仅在设置了 DDSCAPS\_EXECUTEBUFFER 标志时进行调用。 缓冲区创建标志是 DDSCAPS\_WRITEONLY、DDSCAPS2\_VERTEXBUFFER 和 DDSCAPS2\_COMMANDBUFFER。

驱动程序通过检查[**DD\_SURFACE\_本地**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_local)结构传递到**CanCreateExecuteBuffer**的**ddsCaps**成员和**CreateExecuteBuffer**回调来确定所请求的缓冲区类型。以下标志：

-   DDSCAPS\_VERTEXBUFFER 指示驱动程序应分配显式顶点缓冲区。

-   DDSCAPS\_COMMANDBUFFER 指示驱动程序应分配命令缓冲区。

-   如果两个标志均未设置，则驱动程序应分配隐式顶点缓冲区。

驱动程序在内部分配顶点和命令缓冲区，并循环遍历这些缓冲区。 Direct3D 填充给定对，而硬件以异步方式从其他排队缓冲区呈现。 这对于直接内存访问（DMA）非常有用。

Multibuffering 集中的缓冲区可以是不同的内存类型，即系统或视频内存。 调用驱动程序创建第一个缓冲区时，将立即创建该集，并将集中的第一个缓冲区返回到 Direct3D。 驱动程序使用标志来指定用于分配集中的每个缓冲区的内存类型。 如果设置了 D3DHALDP2\_SWAPVERTEXBUFFER 或 D3DHALDP2\_SWAPCOMMANDBUFFER 标志[ **，则驱动**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)程序应在系统内存中为每次调用返回一个新缓冲区。 如果返回的缓冲区位于视频内存中，则应设置相应的 D3DHALDP2\_VIDMEMVERTEXBUF 或 D3DHALDP2\_VIDMEMCOMMANDBUF 标志。

偶尔，Direct3D 会请求下一个缓冲区的最小大小。 如果大小太大，驱动程序应在系统内存（一个后备面）中分配缓冲区。 如果大小太小，则允许该驱动程序提供更大的缓冲区。 驱动程序应跟踪缓冲区数量和内存类型，并在退出时清理所有内容。

 

 





