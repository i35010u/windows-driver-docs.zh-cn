---
title: 从 KMDF 驱动程序突入调试程序
description: 从 KMDF 驱动程序突入调试程序
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- 调试驱动程序 WDK KMDF，中断调试器
- 中断调试器 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c883264ea99f46048cc65b118ebc0308210cb692
ms.sourcegitcommit: 46853426563bfac36651565181d7edac339f63af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74261442"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>从 KMDF 驱动程序突入调试程序


如果希望基于框架的驱动程序分解为内核模式调试器，可以使用以下内容：

-   如果在注册表中设置了[DbgBreakOnError](registry-values-for-debugging-kmdf-drivers.md)值，则[**WdfVerifierDbgBreakPoint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)函数会中断调试器。

-   如果表达式的计算结果为**FALSE** ，并且在注册表中设置了[VerifyOn](registry-values-for-debugging-kmdf-drivers.md)值，则[**WDFVERIFY**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfverify)宏将测试逻辑表达式并中断内核调试器。

-   如果驱动程序未以 IRQL = 被动\_级别执行，并且在注册表中设置了**VerifyOn**值，则[**VERIFY\_将\_IRQL\_被动\_级**](https://docs.microsoft.com/windows-hardware/drivers/wdf/verify-is-irql-passive-level)宏中断进入内核调试器。

-   如果表达式的计算结果为**FALSE**，则[**断言**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))宏会测试逻辑表达式并中断内核调试器。

-   [**ASSERTMSG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)宏可测试表达式，如果表达式的计算结果为**FALSE**，则会中断内核调试器并向调试器提供可显示的文本消息。

-   [**DbgPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)和[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)函数向调试器提供可显示的文本消息。

当你在发布或调试配置中构建驱动程序时，WDFVERIFY 的代码和验证\_是\_IRQL\_被动\_级别的宏包含在你的驱动程序中。 仅当你在调试配置中构建驱动程序时，才会将 ASSERT 和 ASSERTMSG 宏的代码包含在你的驱动程序中。

有关项目配置的详细信息，请参阅[构建驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

 

 





