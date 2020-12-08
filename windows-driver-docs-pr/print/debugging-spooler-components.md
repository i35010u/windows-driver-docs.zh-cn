---
title: 调试后台处理程序组件
description: 调试后台处理程序组件
keywords:
- 调试后台处理程序组件 WDK 打印机
- 后台处理程序组件调试 WDK 打印
- 跟踪消息 WDK 打印机
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: afe85bbec49fe38c97eadf411237f15848cab8e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797329"
---
# <a name="debugging-spooler-components"></a>调试后台处理程序组件

本部分提供有关如何在后台处理程序组件中启用调试消息的信息。 本部分的第一部分列出了后台处理程序组件中使用的调试变量。 您可以使用这些调试变量来导致显示后台处理程序组件中的调试消息。 请注意，您必须使用这些组件的已选中版本。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

本节的第二部分详细介绍了在后台处理程序组件中显示跟踪消息所需的步骤。

> [!NOTE]
> [调试 XPSDrv 打印机驱动程序](debugging-xpsdrv-printer-drivers.md)时有一些特殊的注意事项。

## <a name="displaying-trace-messages-in-a-spooler-component"></a>在后台处理程序组件中显示跟踪消息

下面的过程列出了在 winspool.drv. winspool.drv 的已选中版本中查看跟踪消息所需的步骤。 对于其他后台处理程序组件，显示跟踪消息的步骤是类似的。

若要在后台处理程序组件中显示跟踪消息：

1. 附加调试器。

1. 中断要调试的进程。

1. 找到 debug 变量 winspool.drv！ClientDebug.

1. 将 \_ 0x0008) 中的 DBG 跟踪位设置 (为 winspool.drv！ClientDebug 变量。

1. 单击“转到”。
