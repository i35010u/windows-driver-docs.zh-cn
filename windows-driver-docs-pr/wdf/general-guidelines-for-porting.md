---
title: 准备移植
description: 准备移植
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a93d567e7818626a30411fd1af6bbad402a80daa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814758"
---
# <a name="preparing-for-porting"></a>准备移植


在某些方面，将驱动程序从 WDM 转换为 Windows 驱动程序框架 (WDF) 比移植重新实现更多。 这并不像您所希望的那样困难。 大多数 WDM 驱动程序的特定于硬件的代码可以保持相对完好，尽管它将使用一些不同的对象类型。 WDF 默认值将替换 WDM 驱动程序所需的很多样板代码（特别是对于即插即用），并且 WDF 为驱动程序实现的许多棘手方面提供内置支持，如 i/o 取消 (以及相关联的争用条件) 和系统电源状态转换。

以下一般准则适用于移植驱动程序：

-   请参阅 [示例](/samples/browse/)。 WDF 附带了一组丰富的示例，其中的大多数示例都是名称类似的 WDM 驱动程序的端口。
-   以增量方式工作。 由于该框架为 i/o、即插即用、电源管理和 WMI 请求实现了默认行为，因此你可以一次编码并调试一个设备或驱动程序功能。
-   对于 Kernel-Mode Driver Framework (KMDF) ，实现 WMI 事件跟踪，以提供用于调试的详细跟踪日志。
-   在许多情况下，WDF 默认值提供的功能比现有 WDM 驱动程序实现的功能更多。 在尝试移植复杂代码（特别是对于同步或队列管理）之前，请确保 WDF 提供的内容。 它可能会节省大量用于移植驱动程序的时间。
-   使用 Windows 驱动程序工具包 (WDK) 中包含的特定于 WDF 的 [调试器扩展](debugger-extensions-for-kmdf-drivers.md) 。
-   调试时启用 [KMDF 验证](using-kmdf-verifier.md) 程序或 [UMDF 验证](using-umdf-verifier.md) 程序。

## <a name="wdm-driver-analysis"></a>WDM 驱动程序分析


不管涉及哪种类型的设备和驱动程序，移植驱动程序时最重要的问题是通过驱动程序了解 i/o 流。 开始编写代码之前，请仔细分析现有的 WDM 驱动程序。 你应该能够回答以下问题：

-   驱动程序需要多少个设备对象，哪些驱动程序角色 (FDO，PDO，筛选器) 执行哪些操作？ 几乎在所有情况下，WDF 驱动程序都将使用与 WDM 驱动程序相同的设备对象类型和数量。
-   哪些 i/o 请求必须支持驱动程序？
-   驱动程序需要多少队列来处理这些请求？ 这些队列的特征是什么？
-   I/o 处理的哪些方面可以并发发生，哪些都必须进行序列化？
-   驱动程序完成了哪些 i/o 请求，并向下传递堆栈？

这些问题的答案决定了如何构建 WDF 驱动程序的核心、发生 i/o 处理的位置和时间、驱动程序所需的同步类型以及驱动程序必须创建哪些 WDF 对象来执行 i/o。 如果驱动程序支持硬件，还必须全面了解设备：

-   设备是否产生中断？
-   如果有任何)  (硬件支持，DMA 模型会？ 请注意，如果驱动程序需要 DMA，则必须编写 KMDF 驱动程序。
-   驱动程序管理设备堆栈的电源策略吗？

最后，如果驱动程序支持 WMI (也只 KMDF) ，则必须了解如何收集它导出的数据以及驱动程序所需的 WMI 回调。

 

