---
title: 语言监视器
description: 语言监视器
ms.assetid: 26ba1c22-390a-4187-b67a-3f3497964f8e
keywords:
- 打印监视器 WDK，语言监视器
- 语言监视器 WDK 打印
- 语言监视器 WDK 打印，关于语言监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c4046ffe79c986cfc478bf4b2b32be09a83a85b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843254"
---
# <a name="language-monitors"></a>语言监视器





语言监视器是提供两个用途的用户模式 Dll：

-   它们在打印后台处理程序和双向打印机之间提供了一个完整的双工通信路径，可以提供软件可访问的状态信息。

-   它们将打印机控制信息（如打印机作业语言定义的命令）添加到数据流。

Microsoft 提供了语言监视器 Pjlmon，它支持*打印机作业语言（PJL）* ，并为 PJL 打印机提供双向通信。 此监视器包含在 Microsoft Windows 驱动程序工具包（WDK）中作为[示例语言监视器](sample-language-monitor.md)。

可以编写自定义语言监视器，以支持单向或双向打印机的其他作业控制语言。

语言监视器是可选的，并且只有在打印机的 INF 文件中包含时才与特定打印机类型相关联，如[安装打印监视器](installing-a-print-monitor.md)中所述。

如果在 "打印机属性" 对话框的 "**端口**" 选项卡中清除 "**启用双向支持**" 复选框，则后台处理程序将不会调用语言监视器的[**StartDocPort**](https://docs.microsoft.com/previous-versions/ff562710(v=vs.85))、 [**WritePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-writeport)、 [**EndDocPort**](https://docs.microsoft.com/previous-versions/ff548742(v=vs.85))、 [**GetPrinterDataFromPort**](https://docs.microsoft.com/previous-versions/ff550506(v=vs.85))、 [**ReadPort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-readport)函数。 即使清除了 "**启用双向支持**"，后台处理程序仍将继续调用[**OpenPortEx**](https://docs.microsoft.com/previous-versions/ff559596(v=vs.85))、 [**ClosePort**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-closeport)和[**SendRecvBidiDataFromPort**](https://docs.microsoft.com/previous-versions/ff562071(v=vs.85))函数。 当应用程序在双向通信 API 中调用函数时，"**启用双向支持**" 复选框不会影响对语言监视器的调用。

如果语言监视器与打印机关联，则语言监视器会从打印处理器接收打印机的数据流，对其进行修改，然后将其传递到打印机的端口监视器。 有关详细信息，请参阅[语言和端口监视器交互](language-and-port-monitor-interaction.md)。

**请注意**   语言监视器应始终实现**SendRecvBidiDataFromPort**函数，并将函数的地址包含在[**MONITOR2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitor2)结构的*pfnSendRecvBidiDataFromPort*成员中。

如果语言监视器不支持双向，或请求包含语言监视器不支持的双向架构值，则语言监视器应将调用转发到端口监视器的**SendRecvBidiDataFromPort**函数。

 

 

 




