---
title: 常规设计和实施策略
description: 常规设计和实施策略
keywords:
- 显示驱动程序模型 WDK Windows 2000，策略
- Windows 2000 显示器驱动程序模型 WDK，策略
- 视频微型端口驱动程序 WDK Windows 2000，策略
- 显示驱动程序 WDK Windows 2000，策略
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3136b9359dc93b8d22514e561e01511dc45fa327
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832427"
---
# <a name="general-design-and-implementation-strategies"></a>常规设计和实施策略


## <span id="ddk_general_design_and_implementation_strategies_gg"></span><span id="DDK_GENERAL_DESIGN_AND_IMPLEMENTATION_STRATEGIES_GG"></span>


要设计有效的 Windows 2000 和更高版本的显示驱动程序和视频微型端口驱动程序，请考虑以下策略：

-   修改现有的 Windows 驱动程序工具包 (WDK) 示例驱动程序，该驱动程序是为类似类型的图形适配器设计的，以减少驱动程序的设计时间。

-   使用 C 来编写尽可能多的驱动程序，只在必要时才使用汇编语言来最大限度地利用汇编语言来实现可移植性。 尽管程序集中的编码增加了优化的可能性，但时间和可移植性问题超出了其优势。

-   为管理资源的操作使用视频微型端口驱动程序，执行物理设备内存映射，确保注册输出发生在接近或响应中断的情况下。 微型端口驱动程序用于处理硬件系列中的变体和最大程度地减少显示驱动程序硬件类型依赖项的主要。

有关显示驱动程序编写器感兴趣的其他信息，请参阅 [用于显示驱动程序的图形 DDI 函数](graphics-ddi-functions-for-display-drivers.md)。 本主题及其后面的副标题讨论了所需的图形 DDI 函数（有条件地需要）和显示驱动程序的可选参数。 [Windows 2000 显示器驱动程序模型及其子主题中的视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md) 包含类似于视频微型端口驱动程序编写器的信息。

还应考虑以下事实：

-   显示驱动程序和视频微型端口驱动程序在与 NT 高级管理人员的其余部分相同的特权内核模式地址空间中运行。 任一驱动程序中的错误都将导致系统的其余部分出现故障。

-   可随时抢占显示驱动程序和视频微型端口驱动程序。

-   显示驱动程序的 "代码" 和 "数据" 部分均可完全分页。

-   导出的函数必须在进入时执行基于 NT 的标准操作系统 *prolog* ，并在退出时执行 *epilog* 。 有关详细信息，请参阅 Microsoft Windows SDK 文档。

有关特定于显示驱动程序的信息，请参阅 [用于显示驱动程序的图形 DDI 函数](graphics-ddi-functions-for-display-drivers.md)。 该部分包含有关所需的信息、有条件地需要的信息，以及可选的必需图形 DDI 函数。

 

 





