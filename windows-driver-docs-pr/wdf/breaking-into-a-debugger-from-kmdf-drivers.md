---
title: 从 KMDF 驱动程序突入调试程序
description: 从 KMDF 驱动程序突入调试程序
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- 调试驱动程序 WDK KMDF，中断到调试器
- 中断到调试器 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a156777b1754864705662fbc6bf3c4307edeed7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353220"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>从 KMDF 驱动程序突入调试程序


如果您希望基于 framework 的驱动程序以在内核模式调试器中中断，可以使用以下：

-   [ **WdfVerifierDbgBreakPoint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)函数会中断到调试器，如果[DbgBreakOnError](registry-values-for-debugging-kmdf-drivers.md)在注册表中设置值。

-   [ **WDFVERIFY** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)宏测试的逻辑表达式，并强行进入内核调试器，如果表达式的计算结果**FALSE**如果[VerifyOn](registry-values-for-debugging-kmdf-drivers.md)在注册表中设置值。

-   [**验证\_IS\_IRQL\_被动\_级别**](https://docs.microsoft.com/windows-hardware/drivers/wdf/verify-is-irql-passive-level)宏进入内核调试器如果驱动程序不执行在 IRQL = 被动\_级别; 如果**VerifyOn**在注册表中设置值。

-   [ **ASSERT** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))宏测试的逻辑表达式，并强行进入内核调试器，如果表达式的计算结果**FALSE**。

-   [ **ASSERTMSG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-assertmsg)宏测试表达式和表达式的计算结果**FALSE**、 进入内核调试器，并提供可显示的短信向调试器。

-   [ **DbgPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprintex)并[ **KdPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprintex)函数都提供可显示的短信向调试器。

WDFVERIFY 和验证代码\_IS\_IRQL\_被动\_级别宏包含在您的驱动程序时生成您的版本或调试配置中的驱动程序 (称为免费构建环境或已检验的版本环境在 Windows 7 及更早版本）。 仅当您构建您的驱动程序中的调试配置时，驱动程序中包含的断言和 ASSERTMSG 宏代码。

有关项目配置的详细信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

 

 





