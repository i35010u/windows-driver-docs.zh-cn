---
title: 语言监视器
description: 语言监视器
ms.assetid: 26ba1c22-390a-4187-b67a-3f3497964f8e
keywords:
- 打印监视器 WDK，语言监视器
- 打印语言监视器 WDK
- 打印语言监视器 WDK，有关语言监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dff730dc4167f50d302fb1b9ec83629b77ace5b4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388099"
---
# <a name="language-monitors"></a>语言监视器





语言监视器是用户模式 Dll，有两种用途：

-   它们提供的打印后台处理程序和都能够提供可访问软件的状态信息的双向打印机之间的全双工通信路径。

-   它们将添加打印机控制信息，例如，由打印机作业语言，对数据流定义的命令。

Microsoft 提供了语言监视器，Pjlmon.dll，支持*打印机作业语言 (PJL)*，并提供 PJL 打印机的双向通信。 此监视器包含在 Microsoft Windows 驱动程序工具包 (WDK) 作为[示例语言监视器](sample-language-monitor.md)。

可以编写自定义的语言监视器，以支持其他作业控制语言，单向或双向打印机。

语言监视器是可选的仅与特定打印机类型如果打印机的 INF 文件中包括关联，如中所述[安装打印监视器](installing-a-print-monitor.md)。

如果清除**支持双向**中的复选框**端口**选项卡的打印机属性对话框中，后台处理程序将不会调用[ **StartDocPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562710)， [ **WritePort**](https://msdn.microsoft.com/library/windows/hardware/ff563792)， [ **EndDocPort**](https://msdn.microsoft.com/library/windows/hardware/ff548742)， [ **GetPrinterDataFromPort**](https://msdn.microsoft.com/library/windows/hardware/ff550506)， [ **ReadPort** ](https://msdn.microsoft.com/library/windows/hardware/ff561909)函数的语言监视器。 后台处理程序将继续调用[ **OpenPortEx**](https://msdn.microsoft.com/library/windows/hardware/ff559596)， [ **ClosePort**](https://msdn.microsoft.com/library/windows/hardware/ff545975)， [ **SendRecvBidiDataFromPort** ](https://msdn.microsoft.com/library/windows/hardware/ff562071)函数，即使**启用的双向支持**清除。 **启用的双向支持**复选框不会影响当应用程序中的双向通信 API 调用的函数所做的调用到语言监视器。

如果与打印机相关联的语言监视器，语言监视器从打印处理器接收打印机的数据流，修改它，并将其传递到打印机的端口监视器。 有关详细信息，请参阅[语言和端口监视器交互](language-and-port-monitor-interaction.md)。

**请注意**  语言监视器始终应实现**SendRecvBidiDataFromPort**函数，并包含在函数的地址*pfnSendRecvBidiDataFromPort*成员[ **MONITOR2** ](https://msdn.microsoft.com/library/windows/hardware/ff557532)结构。

语言监视器，如果语言监视器不支持 Bidi，或该请求包含 Bidi 架构语言监视器不支持的值，应将转发到端口监视器调用**SendRecvBidiDataFromPort**函数。

 

 

 




