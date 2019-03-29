---
title: 调试后台处理程序组件
description: 调试后台处理程序组件
ms.assetid: ed4dcd29-105c-4562-9741-858cb9542449
keywords:
- 调试后台处理程序组件 WDK 打印机
- 后台处理程序组件调试 WDK 打印
- 跟踪消息 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5a98123f71cbfb90b9473edd7a78086e714383f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569350"
---
# <a name="debugging-spooler-components"></a>调试后台处理程序组件





本部分提供有关如何启用后台处理程序组件中的调试消息的信息。 本部分中的第一个部分列出了在后台处理程序组件中使用的调试变量。 您可以使用这些调试以便于使调试消息发起后台处理程序组件中显示的变量。 （请注意，与选中，您必须使用生成这些组件。）

本部分详细介绍步骤的第二部分需要后台处理程序组件中显示跟踪消息。

**请注意**  有特殊注意事项[调试 XPSDrv 的打印机驱动程序](debugging-xpsdrv-printer-drivers.md)。

 

### <a name="displaying-trace-messages-in-a-spooler-component"></a>在后台处理程序组件中显示跟踪消息

以下过程列出 winspool.drv 的生成步骤，你会看到在检查跟踪消息所必需的。 用于显示跟踪消息的步骤是类似于其他后台处理程序组件。

若要显示跟踪后台处理程序组件中的消息：

1.  附加调试器。

2.  进入想要调试此的进程。

3.  查找调试变量，winspool ！ClientDebug。

4.  设置 DBG\_跟踪位 (0x0008) 中的低位字的 winspool ！ClientDebug 变量。

5.  单击 Go。

 

 




