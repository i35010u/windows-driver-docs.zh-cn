---
title: 开始使用 UMDF
description: 本部分介绍用户模式驱动程序框架 (UMDF)，并详细介绍了 UMDF 版本 1 和 2 之间的差异。
ms.assetid: 2C4DAFA4-783C-4739-8D27-A417AC63B447
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9f65853badd7a6967387206e00d5f173ec9a812
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520499"
---
# <a name="getting-started-with-umdf"></a>开始使用 UMDF


本部分介绍用户模式驱动程序框架 (UMDF)，并详细介绍了 UMDF 版本 1 和 2 之间的差异。 它还提供有关 UMDF 的高级体系结构信息。 若要确定 UMDF 驱动程序是否适合你的需求，并决定要使用的 UMDF 版本，请使用此部分。

Windows 驱动程序框架 (WDF) 包含 UMDF，一个框架，用于创建用户模式驱动程序。 如内核模式驱动程序框架 (KMDF)，UMDF 从 WDM，处理大量插即用 (PnP) 和电源管理功能，并允许该驱动程序来选择加入特定功能和事件处理提供一个抽象层。

在 Windows 8.1 之后，有两个主要版本的 UMDF，版本 1 和 2。 UMDF 版本 1.11 （十一一个圆点） 是 UMDF 版本 1，最新版本，是 UMDF 2 出现之前的最终版本。 显示完整的版本信息和操作系统相关性的表格，请参阅[UMDF 版本历史记录](umdf-version-history.md)。

编写使用 UMDF 版本 1 需要使用 COM 编程模型编写 c + + 代码的驱动程序。 而 UMDF 版本 1 基于 KMDF 与相同的概念的驱动程序编程模型，UMDF 1 实现具有不同的组件、 设备驱动程序接口 (DDIs) 和数据结构的模型。

与此相反，您可以从 UMDF 版本 2 开始，在调用的许多方法可用于 KMDF 驱动程序的 C 编程语言中编写 UMDF 驱动程序。 所有版本 2 UMDF 和 KMDF 之间共享的接口具有相同的名称、 参数和结构定义。 如果您的驱动程序仅使用共享的功能，或使用仅支持在一个框架中的调用周围的条件性宏，您可以编写单个驱动程序可以使用 KMDF 或 UMDF 编译。 有关详细信息，请参阅[如何从 KMDF 驱动程序生成 UMDF 驱动程序](how-to-generate-a-umdf-driver-from-a-kmdf-driver.md)。

虽然 UMDF 2 和 KMDF 之间的重大通用性，就仍有少量的仅在一个框架或其他中可用的功能。 有关详细信息，请参阅[比较 UMDF 2 功能提供给 KMDF](comparing-umdf-2-0-functionality-to-kmdf.md)。 有关所有 UMDF 2 和 KMDF 回调和方法的列表和它们适用于，哪个框架请参见[WDF 回调摘要和方法](https://msdn.microsoft.com/library/windows/hardware/dn265591)。 在少数情况下，结构成员或方法的参数仅适用于一个框架或其他。 文档上相应的参考页介绍这些差异。

必须选择一个或另一种;无法写入 UMDF 驱动程序从这两种 UMDF 版本 1 和 2 中调用方法。

UMDF 版本 2 的驱动程序运行仅在 Windows 8.1 或更高版本。 如果您需要编写在操作系统运行早于 Windows 8.1 的 UMDF 驱动程序，需要编写 UMDF 1.x 驱动程序。 可以使用版本 1.11 构建运行 Windows Vista 及更高版本的驱动程序。 版本 1 的详细信息，请参阅[UMDF 1.x 设计指南](user-mode-driver-framework-design-guide.md)。 本部分介绍 UMDF 版本 2。



 

 
