---
title: 常规设计和实施策略
description: 常规设计和实施策略
ms.assetid: c631062c-87ec-4bad-9de2-1844d0c81661
keywords:
- 显示器驱动程序模型 WDK Windows 2000 中，策略
- Windows 2000 显示器驱动程序模型 WDK，策略
- 微型端口驱动程序 WDK Windows 2000 中，策略
- 显示驱动程序 WDK Windows 2000 中，策略
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0589881083b5c32dbc2ecca9cd5e0e01ec20e6d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377974"
---
# <a name="general-design-and-implementation-strategies"></a>常规设计和实施策略


## <span id="ddk_general_design_and_implementation_strategies_gg"></span><span id="DDK_GENERAL_DESIGN_AND_IMPLEMENTATION_STRATEGIES_GG"></span>


若要设计有效的 Windows 2000 和更高版本显示驱动程序和视频的微型端口驱动程序，请考虑以下策略：

-   修改现有的 Windows Driver Kit (WDK) 示例驱动程序的相似类型的图形适配器设计用于减少驱动程序设计时。

-   使用 C 来尽可能以最大化可移植性，使用程序集语言仅在必要也不支持的硬件的严格要求时间的操作时写入尽可能多的驱动程序。 虽然在程序集编码会增加优化的可能性，但是时间和可移植性问题超过它的好处。

-   使用的操作管理资源、 执行物理设备内存映射，请确保输出响应的中断或邻近，发生了注册的微型端口驱动程序。 微型端口驱动程序是主要是用于处理硬件系列中的变体和最小化显示驱动程序硬件类型依赖关系。

以显示驱动程序编写人员感兴趣的其他信息，请参阅[图形 DDI 函数显示驱动程序](graphics-ddi-functions-for-display-drivers.md)。 本主题和其后的子主题讨论了图形 DDI 函数的必需、 有条件地必需和可选的显示驱动程序。 [在 Windows 2000 显示器驱动程序模型中的视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)和及其子主题包含针对的微型端口驱动程序编写人员是类似的信息。

你还应考虑以下事实：

-   显示驱动程序和视频的微型端口驱动程序运行在与 NT 高级管理人员的其余部分相同的特权的内核模式地址空间中。 任一驱动程序中的错误将导致错误系统的其余部分。

-   显示驱动程序和视频的微型端口驱动程序可以在任何时候被抢占。

-   显示驱动程序的代码和数据部分都完全可分页。

-   导出的函数必须执行标准的基于 NT 的操作系统*prolog*条目并*epilog*退出。 有关详细信息，请参阅 Microsoft Windows SDK 文档。

特定于显示驱动程序的信息，请参阅[图形 DDI 函数显示驱动程序](graphics-ddi-functions-for-display-drivers.md)。 该部分包含有关所需、 按条件必需的且可以选择所需的图形 DDI 函数的信息。

 

 





