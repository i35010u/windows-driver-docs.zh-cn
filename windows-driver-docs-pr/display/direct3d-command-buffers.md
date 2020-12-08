---
title: Direct3D 命令缓冲区
description: Direct3D 命令缓冲区
keywords:
- 命令缓冲区 WDK Direct3D
- 缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d3b05bed69734da1bc3516bd6efd5175f839c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809507"
---
# <a name="direct3d-command-buffers"></a>Direct3D 命令缓冲区


## <span id="ddk_direct3d_command_buffers_gg"></span><span id="DDK_DIRECT3D_COMMAND_BUFFERS_GG"></span>


下图显示了一个示例逻辑命令缓冲区的部分。 驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调接收指向 [**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的 **lpDDCommands** 成员中的命令缓冲区的指针。 命令缓冲区始终按顺序处理。

![说明 direct3d 示例逻辑命令缓冲区的部分的示意图](images/d3dcmbuf.png)

如上图所示，命令缓冲区包含 [**D3DHAL \_ DP2COMMAND**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command) 结构，其中每个结构的 **bCommand** 成员标识一个命令。 下面列出了可能的命令：

-   D3DDP2OP \_ RENDERSTATE 指示在命令缓冲区中跟随 **wStateCount**[**D3DHAL \_ DP2RENDERSTATE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate) 结构。 驱动程序应该分析每个结构的状态，并相应地更新其私有驱动程序状态。 驱动程序还应将数组中的相应状态更新为 **lpdwRStates** 点。 如果驱动程序不支持命令缓冲区中请求的状态，驱动程序应该用它支持的值覆盖请求的值。

-   D3DDP2OP \_ TEXTURESTAGESTATE 指示在命令缓冲区中跟随 **wStateCount**[**D3DHAL \_ DP2TEXTURESTAGESTATE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate) 结构。 驱动程序应该分析每个结构的状态，并相应地更新与指定纹理阶段相关联的驱动程序的纹理状态。 该驱动程序不会向 Direct3D 运行时报告纹理阶段状态。

    无论实际使用的坐标集有多少，驱动程序都需要正确分析八个纹理坐标集。

-   D3DDP2OP \_ VIEWPORTINFO 指示在命令缓冲区后面有一个 [**D3DHAL \_ DP2VIEWPORTINFO**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo) 结构。 驱动程序应分析此结构并更新存储在驱动程序的内部呈现上下文中的视区信息。

-   D3DDP2OP \_ WINFO 指示在命令缓冲区后面有一个 [**D3DHAL \_ DP2WINFO**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2winfo) 结构。 驱动程序应分析此结构并更新存储在驱动程序的内部呈现上下文中的 w 缓冲区信息。

-   其余的 D3DDP2OP \_ *Xxx* 命令指示在命令缓冲区中有足够的数据来呈现 **wPrimitiveCount** ([**D3DHAL \_ DP2COMMAND**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构) 基元的成员。 根据基元命令，驱动程序应 \_ 从命令缓冲区和顶点缓冲区和命令缓冲区中的一个或两个顶点关联的数据分析 D3DHAL DP2 *Xxx* 结构。 驱动程序必须尝试处理所有有效的 D3DDP2OP \_ *Xxx* 命令; 即，驱动程序无法选择忽略某些已定义的基元类型。 有关详细信息，请参阅 D3DHAL \_ DP2 *Xxx* 结构参考页。

根据当前命令，以下附加信息存储在命令缓冲区中：

-   所有 D3DDP2OP \_ 索引 *Xxx* 基元命令的索引信息。

-   D3DDP2OP \_ TRIANGLEFAN \_ IMM 和 D3DDP2OP \_ LINELIST \_ imm 基元命令的顶点数据。

-   其他操作也 \_ 在 [**D3DHAL \_ DP2OPERATION**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)结构中定义为 D3DDP2OP *Xxx* 操作码。 它们等效于 \_ 具有相同名称的 D3DDP2OP *Xxx* 命令。

命令缓冲区偶尔包含只有 Direct3D 才能理解的命令。 如果驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 回调不识别该命令，则驱动程序应调用 Direct3D's **D3dParseUnknownCommand** 回调来尝试对其进行分析。 当 **D3dParseUnknownCommand** 成功返回时，驱动程序应继续分析并处理命令缓冲区。 如果 **D3dParseUnknownCommand** 通过返回未分析的 D3DERR \_ 命令失败，则 \_ **D3dDrawPrimitives2** 应设置 [**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data) 结构的以下成员并返回：

-   在 **dwErrorOffset** 中，写入第一个未处理的 [**D3DHAL \_ DP2COMMAND**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command) 结构的偏移量，该结构是 **lpDDCommands** 指向的缓冲区的一部分。

-   将 **ddrval** 设置为未分析的 D3DERR \_ 命令 \_ 。

有关如何初始化 **D3dParseUnknownCommand** 回调的信息，请参阅 [Direct3D 驱动程序初始化](direct3d-driver-initialization.md)。

为了简化 **D3dDrawPrimitives2** 的实现，驱动程序编写者可以从 *Perm3* 示例代码复制分析代码，并仅编写驱动程序特定的呈现和状态更新代码。

**注意**   Microsoft Windows 驱动程序工具包 (WDK) 不包含 *Perm3*)  (的 3Dlabs Permedia3 示例显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包获取此示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载该驱动程序。

 

并非始终向 Direct3D 通知当前的呈现状态。 例如，运行时不会在执行缓冲区到达驱动程序之前对其进行检查。 驱动程序可以跟踪呈现器状态数组和 [**D3DHAL \_ DRAWPRIMITIVES2DATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的 **lpdwRStates** 成员。 这是一个指针，指向在发生状态更改时驱动程序保持最新状态的内部呈现状态数组。

 

