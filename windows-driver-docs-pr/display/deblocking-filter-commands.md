---
title: 除块筛选器命令
description: 除块筛选器命令
ms.assetid: 9f20c6fa-c515-43b8-a947-f6290d15bd35
keywords:
- 宏块 WDK DirectX VA，消除马赛克功能筛选器的命令
- 消除马赛克功能筛选命令 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1663b1c9814bc5c8b7b9193960c3d7c2a668f2c8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358651"
---
# <a name="deblocking-filter-commands"></a>除块筛选器命令


## <span id="ddk_deblocking_filter_commands_gg"></span><span id="DDK_DEBLOCKING_FILTER_COMMANDS_GG"></span>


宏块的 deblocking 筛选器命令可能需要读取的值重新构造的示例中，加速器和到当前宏块的下一步。 读取的重新构造的值是当前宏块，上面的示例的当前宏块，左侧的示例和示例在当前宏块内的两个列的两个行。 Deblocking 的筛选器命令可能会导致对一个行的当前宏块上面的示例和示例留下的当前宏块，以及最多三个行的一列和三个列的当前宏块中的示例的修改。 消除马赛克功能筛选给定宏块的进程，因此，需要其他两个宏块之前重新的构造。

两种不同类型的筛选器的命令缓冲区消除马赛克功能是：

-   需要访问和修改的值的缓冲区重新构造外的当前筛选器 deblocking 命令缓冲区宏块的示例 (当**bPicDeblockConfined**的成员[ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)结构为零)。

-   不需要访问和修改的值的缓冲区重新构造外的当前筛选器 deblocking 命令缓冲区宏块的示例 (当**bPicDeblockConfined**为 1)。

若要处理的第一种消除马赛克功能命令缓冲区，快捷键必须确保宏块重新构造已为影响块效应向左或更高版本在当前缓冲区中，控制块效应的所有缓冲区。 这必须处理当前缓冲区中的 deblocking 命令之前完成。

若要处理的命令缓冲区消除马赛克功能的第二个类型，快捷键，请使用仅以前的重新构造当前缓冲区中的值。

可以通过两种方式之一 accelerator 中执行 deblocking 的筛选器操作：

-   处理整个缓冲区或框架的动作预测和剩余差异数据首先后, 跟返回中的某些示例值读取和由于 deblocking 的筛选器操作而对其进行修改。

-   采用协调的方式与剩余的差异数据缓冲区处理 deblocking 命令缓冲区。 在这种情况下，deblocking 命令缓冲区进行处理然后再重新构造的输出值写入目标图面。

**请注意**   deblocked 图片目标图面上可能有所不同，消除马赛克功能之前重新构造的图片。 然后，这可以支持"外部循环"消除马赛克功能作为 postdecoding 进程的未影响用于预测下一张图片的示例值。

 

 

 





