---
title: 消除马赛克功能筛选器控件
description: 消除马赛克功能筛选器控件
ms.assetid: b332421e-da15-4c42-aedb-32f4ba24101e
keywords:
- 宏块 WDK DirectX VA，消除马赛克功能筛选器控件
- 消除筛选器控件 WDK DirectX VA 马赛克功能
- 色度预测阻止 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83355c2bdaf029b2cc517b33cd3e932452eb3476
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523051"
---
# <a name="deblocking-filter-control"></a>消除马赛克功能筛选器控件


## <span id="ddk_deblocking_filter_control_gg"></span><span id="DDK_DEBLOCKING_FILTER_CONTROL_GG"></span>


消除马赛克功能筛选器控制命令 （如果存在） 为每个宏块中的亮度块发送一次和色度块的每个对发送一次。 筛选器控制命令宏块内的光栅扫描顺序发送。 筛选器控制命令发送的亮度色度任何阻塞之前的所有块。 筛选器控制命令随后会发送一个色度 4:2:0 块，然后为一个色度 4:2:2 块 (如果 4:2:2 正在使用中)，然后针对两个色度 4:4： 如果需要 4 个命令 (相同的筛选将应用于这两种色度*组件*).

对每个块的筛选是通过指定消除马赛克在块中后, 跟消除马赛克功能在块的左边缘之间的上边缘之间的功能。 消除马赛克功能为色度只能指定一次，并 Cb 和 Cr 分量使用相同的 deblocking 命令。 例如，包含 4 16x16 宏块的消除马赛克功能： 使用 8x8 块 2:0 数据通过发送完成四个两个 （顶部和左侧） 边缘滤波命令集的亮度块后, 接一组的两个色度的两个边缘滤波命令块。

 

 





