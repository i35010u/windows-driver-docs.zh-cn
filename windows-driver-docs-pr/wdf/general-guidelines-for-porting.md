---
title: 为迁移准备
description: 为迁移准备
ms.assetid: 355CD834-6B64-4E6F-AA17-AE1145F269CA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b8e6378c1812d196336edfa63c8fed3b69252b9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534203"
---
# <a name="preparing-for-porting"></a>为迁移准备


在某些方面，将从 WDM 驱动程序转换到 Windows 驱动程序框架 (WDF) 是比移植的多个重新实现。 这是既不像难，也不为耗时，正如您所料。 尽管它将使用一些不同的对象类型，大部分 WDM 驱动程序的特定于硬件的代码可以保持相对较不变。 WDF 默认值替换的样板代码的 WDM 驱动程序需要很多 — 特别是对于插 — 和 WDF 驱动程序实现，如 I/O 取消 （和相关联的争用条件） 的许多复杂方面提供了内置支持和系统电源状态转换。

遵循以下通用原则适用于移植驱动程序：

-   请参阅[示例](https://go.microsoft.com/fwlink/p/?linkid=256387)。 WDF 附带了一套丰富的示例，其中大部分是类似的命名 WDM 驱动程序的端口。
-   以增量方式工作。 由于框架的 I/O、 插、 电源管理和 WMI 请求实现默认行为，因此可以代码并一次调试一个设备或驱动程序功能。
-   有关内核模式驱动程序框架 (KMDF)，实现 WMI 事件跟踪来用于调试提供详细的跟踪日志。
-   在许多情况下，WDF 默认值提供更强大的功能比现有 WDM 驱动程序可能已实现。 再到端口尝试复杂的代码 — 尤其是为同步或队列管理 — 一定 WDF 提供。 它可以节省相当长的移植驱动程序所用的时间。
-   使用特定于 WDF 的[调试器扩展](debugger-extensions-for-kmdf-drivers.md)包括 Windows Driver Kit (WDK) 中。
-   启用[KMDF verifier](using-kmdf-verifier.md)或[UMDF verifier](using-umdf-verifier.md)调试时。

## <a name="wdm-driver-analysis"></a>WDM 驱动程序分析


而不考虑设备和驱动程序所涉及的类型，在移植驱动程序最重要的问题是了解通过该驱动程序的 I/O 流。 在开始编写代码之前，仔细分析现有 WDM 驱动程序。 您应该能够回答以下问题：

-   该驱动程序需要多少设备对象，和哪些驱动程序角色 （FDO，PDO，筛选器执行操作） 它们表示？ 在几乎所有情况下，WDF 驱动程序将作为 WDM 驱动程序使用相同的类型和数量的设备对象。
-   I/O 请求必须的驱动程序支持？
-   该驱动程序为这些请求需要多少队列？ 这些队列的特征是什么？
-   I/O 处理的方面可以同时发生，并必须序列化的？
-   驱动程序不会完成，以及其中它 pass 堆栈的下层时的 I/O 请求？

这些问题的答案确定如何构建 WDF 驱动程序的核心、 位置和时间发生了 I/O 处理，哪种类型的同步要求驱动程序，并驱动程序来执行 i/o 操作而必须创建哪些 WDF 对象。 如果该驱动程序支持的硬件，您必须也全面了解设备：

-   设备是否生成中断？
-   在硬件支持哪些 DMA 模型 （如果有）？ 请注意，是否您的驱动程序需要 DMA，您必须编写 KMDF 驱动程序。
-   该驱动程序是否管理设备堆栈的电源策略？

最后，如果该驱动程序支持 WMI (还 KMDF 仅)，则必须了解如何收集它导出和哪些 WMI 回调驱动程序需要的数据。

 

 





