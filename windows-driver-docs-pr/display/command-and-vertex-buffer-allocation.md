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
ms.openlocfilehash: 088c41de521d58de856a824838861aef91769339
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716960"
---
# <a name="command-and-vertex-buffer-allocation"></a>命令和顶点缓冲区分配


## <span id="ddk_command_and_vertex_buffer_allocation_gg"></span><span id="DDK_COMMAND_AND_VERTEX_BUFFER_ALLOCATION_GG"></span>


Direct3D 中使用三种类型的缓冲区：

-   仅供内部使用的隐式顶点缓冲区;也就是说，应用程序不能识别它们。 一个隐式顶点缓冲区始终在上下文创建后创建，而 Direct3D 将顶点数据存储在其中。

-   显式顶点缓冲区，只为响应应用程序请求而创建。 然后，Direct3D 会在显式顶点缓冲区中存储顶点数据。

-   仅供内部使用的命令缓冲区;也就是说，应用程序不知道命令缓冲区。 Direct3D 将命令数据存储在命令缓冲区中。

隐式顶点缓冲区是 Direct3D 用于批处理的特殊顶点缓冲区。 它们是在设备初始化期间创建的，并且可以是 multibuffered。 它们始终是可读/写的，因此不应将它们放在 Microsoft DirectX 6.0 和更高版本的视频内存 (中) 。 这种类型的缓冲区标记为缺少 DDSCAPS2 \_ VERTEXBUFFER 和 DDSCAPS2 \_ COMMANDBUFFER 标志。

显式顶点缓冲区由应用程序创建和控制。 除非设置了 DDSCAPS WRITEONLY 标志，否则无法 multibuffered，并且无法将其放入本地或非本地视频内存 \_ 。 显式顶点缓冲区标记有 DDSCAPS \_ VERTEXBUFFER。

Direct3D 用于批处理命令的命令缓冲区。 它们可以是 multibuffered，可用于除 TLVERTEX 或未剪辑执行缓冲区调用之外的所有 Api。 此类型的缓冲区由标记 DDSCAPS2 \_ COMMANDBUFFER 标记。 它们始终是只写的，但未设置显式标志并且它们从不包含无效的指令。

默认情况下，Direct3D 运行时分配所有这些缓冲区。 可以通过与它们关联的图面来访问隐式顶点缓冲区和命令缓冲区。 所有缓冲区都将传递给驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 回调。

### <a name="span-iddriver-allocated_vertex_and_command_buffersspanspan-iddriver-allocated_vertex_and_command_buffersspanspan-iddriver-allocated_vertex_and_command_buffersspandriver-allocated-vertex-and-command-buffers"></a><span id="Driver-Allocated_Vertex_and_Command_Buffers"></span><span id="driver-allocated_vertex_and_command_buffers"></span><span id="DRIVER-ALLOCATED_VERTEX_AND_COMMAND_BUFFERS"></span>驱动程序分配的顶点和命令缓冲区

Direct3D 驱动程序可通过提供回调函数来选择执行顶点和命令缓冲区分配。 为了提供这些回调函数，Direct3D 驱动程序会填写[**dd \_ D3DBUFCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_d3dbufcallbacks)结构，并将[**Dd \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**lpD3DBufCallbacks**成员指向该结构。 DD \_ HALINFO 由 [**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo) 返回，以响应驱动程序的 DirectDraw 组件的初始化。 DD D3DBUFCALLBACKS 结构中报告的回调 \_ 为：

-   [*CanCreateD3DBuffer*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_cancreatesurface)

-   [*CreateD3DBuffer*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurface)

-   [*DestroyD3DBuffer*](/previous-versions/windows/hardware/drivers/ff552754(v=vs.85))

-   [*LockD3DBuffer*](/previous-versions/windows/hardware/drivers/ff568216(v=vs.85))

-   [*UnlockD3DBuffer*](/previous-versions/windows/hardware/drivers/ff570106(v=vs.85))

这些函数的调用方式与 *DdXxxSurface* 回调 (例如 [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))) ，并且仅在设置了 DDSCAPS EXECUTEBUFFER 标志时进行调用 \_ 。 缓冲区创建标志为 DDSCAPS \_ WRITEONLY、DDSCAPS2 \_ VERTEXBUFFER 和 DDSCAPS2 \_ COMMANDBUFFER。

驱动程序通过检查为以下标志传递到**CanCreateExecuteBuffer**和**CreateExecuteBuffer**回调的[**DD \_ SURFACE \_ 本地**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_local)结构的**ddsCaps**成员来确定所请求的缓冲区类型：

-   DDSCAPS \_ VERTEXBUFFER 指示驱动程序应分配显式顶点缓冲区。

-   DDSCAPS \_ COMMANDBUFFER 指示驱动程序应分配命令缓冲区。

-   如果两个标志均未设置，则驱动程序应分配隐式顶点缓冲区。

驱动程序在内部分配顶点和命令缓冲区，并循环遍历这些缓冲区。 Direct3D 填充给定对，而硬件以异步方式从其他排队缓冲区呈现。 这对于 (DMA) 的直接内存访问很有用。

Multibuffering 集中的缓冲区可以是不同的内存类型，即系统或视频内存。 调用驱动程序创建第一个缓冲区时，将立即创建该集，并将集中的第一个缓冲区返回到 Direct3D。 驱动程序使用标志来指定用于分配集中的每个缓冲区的内存类型。 如果设置了 D3DHALDP2 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) \_ SWAPVERTEXBUFFER 或 D3DHALDP2 \_ SWAPCOMMANDBUFFER 标志，则驱动程序应在系统内存中为每次调用 D3dDrawPrimitives2 返回一个新缓冲区。 如果返回的缓冲区位于视频内存中，则应设置相应的 D3DHALDP2 \_ VIDMEMVERTEXBUF 或 D3DHALDP2 \_ VIDMEMCOMMANDBUF 标志。

偶尔，Direct3D 会请求下一个缓冲区的最小大小。 如果大小太大，驱动程序应在系统内存中分配缓冲区)  (后备面。 如果大小太小，则允许该驱动程序提供更大的缓冲区。 驱动程序应跟踪缓冲区数量和内存类型，并在退出时清理所有内容。

 

