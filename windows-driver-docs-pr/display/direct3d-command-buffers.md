---
title: Direct3D 命令缓冲区
description: Direct3D 命令缓冲区
ms.assetid: d8c093fa-da5c-497c-9eb8-4f689eb96cbf
keywords:
- 命令缓冲区 WDK Direct3D
- WDK Direct3D 缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5092a069e854cd7072bac69b53997e4e1f9d19d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384874"
---
# <a name="direct3d-command-buffers"></a>Direct3D 命令缓冲区


## <span id="ddk_direct3d_command_buffers_gg"></span><span id="DDK_DIRECT3D_COMMAND_BUFFERS_GG"></span>


下图显示了部分示例逻辑命令缓冲区。 在驱动程序[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调接收指向中的命令缓冲区**lpDDCommands**隶属[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构。 命令缓冲区始终按顺序处理。

![说明的 direct3d 示例逻辑命令缓冲区部分的关系图](images/d3dcmbuf.png)

在上图中所示，包含命令缓冲区[ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构，其中**bCommand**的每个结构成员将命令标识。 下面的列表可能命令：

-   D3DDP2OP\_RENDERSTATE 指示已**wStateCount**[**D3DHAL\_DP2RENDERSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2renderstate)按照在命令中的结构缓冲区。 该驱动程序应分析从每个这些结构的状态，并相应地更新其专用驱动程序状态。 驱动程序还应在数组中相应的状态更新到**lpdwRStates**点。 如果该驱动程序不支持请求的命令缓冲区中的状态，该驱动程序应重写其中一个支持请求的值。

-   D3DDP2OP\_TEXTURESTAGESTATE 指示已**wStateCount**[**D3DHAL\_DP2TEXTURESTAGESTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)结构后面中的命令缓冲区。 该驱动程序应分析从每个这些结构的状态，并更新相应地与指定的纹理阶段相关联的驱动程序的纹理状态。 该驱动程序不报告纹理阶段状态返回到 Direct3D 运行时。

    驱动程序是所需正确实际上使用最多八个纹理坐标集，而不考虑多少坐标将其设置的分析。

-   D3DDP2OP\_VIEWPORTINFO 指示一个[ **D3DHAL\_DP2VIEWPORTINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2viewportinfo)命令缓冲区中的结构。 该驱动程序应分析此结构，并更新存储在驱动程序的内部呈现上下文中的视区信息。

-   D3DDP2OP\_WINFO 指示一个[ **D3DHAL\_DP2WINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2winfo)命令缓冲区中的结构。 该驱动程序应分析此结构，并更新驱动程序的内部呈现上下文中存储的 w 缓冲区信息。

-   任何剩余 D3DDP2OP\_*Xxx*命令指示是在要呈现的命令缓冲区足够数据以下**wPrimitiveCount** (隶属[ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构) 的基元。 具体取决于基元命令，该驱动程序应分析 D3DHAL\_DP2*Xxx*来自命令缓冲区和从顶点关联的数据或顶点缓冲区和命令缓冲区的结构。 该驱动程序必须尝试处理所有有效 D3DDP2OP\_*Xxx*命令; 也就是说，该驱动程序不能选择忽略某些定义的基元类型。 有关详细信息，请参阅各个 D3DHAL\_DP2*Xxx*结构参考页。

具体取决于当前命令，命令缓冲区中存储的以下附加信息：

-   索引信息的所有 D3DDP2OP\_INDEXED*Xxx*基元命令。

-   顶点数据 D3DDP2OP\_TRIANGLEFAN\_IMM 和 D3DDP2OP\_LINELIST\_IMM 基元命令。

-   其他操作也被定义为 D3DDP2OP\_*Xxx*中的操作码[ **D3DHAL\_DP2OPERATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ne-d3dhal-_d3dhal_dp2operation)结构。 这些是等效于 D3DDP2OP\_*Xxx*具有相同名称的命令。

命令缓冲区有时包含仅由 Direct3D 理解的命令。 如果驱动程序的[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调无法识别该命令，该驱动程序应调用 Direct3D 的**D3dParseUnknownCommand**要尝试回调对其进行分析。 当**D3dParseUnknownCommand**成功，返回该驱动程序应继续分析和处理命令缓冲区。 如果**D3dParseUnknownCommand**失败并返回 D3DERR\_命令\_未分析， **D3dDrawPrimitives2**应设置的以下成员[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构，并返回：

-   在中**dwErrorOffset**，写入的偏移量的第一个未处理[ **D3DHAL\_DP2COMMAND** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构，它是到缓冲区的一部分**lpDDCommands**点。

-   设置**ddrval**到 D3DERR\_命令\_UNPARSED。

有关如何初始化**D3dParseUnknownCommand**回调，请参阅[Direct3D 驱动程序初始化](direct3d-driver-initialization.md)。

若要简化的实现**D3dDrawPrimitives2**，驱动程序编写人员可以将复制从分析的代码*Perm3*示例代码和编写特定于驱动程序的呈现和状态更新仅适用于代码。

**请注意**   Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia3 示例显示器驱动程序 (*Perm3.h*)。 你可以获取从 Windows Server 2003 SP1 驱动程序开发工具包 (DDK)，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载此示例驱动程序。

 

Direct3D 不会始终通知的当前的呈现状态。 例如，执行到达该驱动程序之前，由运行时不检查缓冲区。 该驱动程序可以跟踪的呈现状态数组**lpdwRStates**的成员[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构。 这是指向发生状态更改时，该驱动程序保持最新的内部呈现状态数组的指针。

 

 





