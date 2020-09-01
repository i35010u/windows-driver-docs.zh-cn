---
title: 从 KMDF 驱动程序突入调试程序
description: 从 KMDF 驱动程序突入调试程序
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- 调试驱动程序 WDK KMDF，中断调试器
- 中断调试器 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2465579fa6616c68196b8d89beedd4d46626cd39
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184041"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>从 KMDF 驱动程序突入调试程序


如果希望基于框架的驱动程序分解为内核模式调试器，可以使用以下内容：

-   如果在注册表中设置了[DbgBreakOnError](registry-values-for-debugging-kmdf-drivers.md)值，则[**WdfVerifierDbgBreakPoint**](/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierdbgbreakpoint)函数会中断调试器。

-   如果表达式的计算结果为**FALSE** ，并且在注册表中设置了[VerifyOn](registry-values-for-debugging-kmdf-drivers.md)值，则[**WDFVERIFY**](./wdfverify.md)宏将测试逻辑表达式并中断内核调试器。

-   如果驱动程序未在 IRQL = 被动级别执行，并且在注册表中设置了 VerifyOn 值，则[**验证 \_ 为 \_ irql \_ 被动 \_ 级别**](./verify-is-irql-passive-level.md)宏中断进入内核调试器 \_ 。 **VerifyOn**

-   如果表达式的计算结果为**FALSE**，则[**断言**](/previous-versions/windows/hardware/previsioning-framework/ff542107(v=vs.85))宏会测试逻辑表达式并中断内核调试器。

-   [**ASSERTMSG**](/windows-hardware/drivers/ddi/wdm/nf-wdm-assertmsg)宏可测试表达式，如果表达式的计算结果为**FALSE**，则会中断内核调试器并向调试器提供可显示的文本消息。

-   [**DbgPrintEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)和[**KdPrintEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)函数向调试器提供可显示的文本消息。

\_ \_ \_ \_ 当你在发布或调试配置中构建驱动程序时，你的驱动程序中将包含 WDFVERIFY 和 VERIFY 的代码为 IRQL 被动级别宏。 仅当你在调试配置中构建驱动程序时，才会将 ASSERT 和 ASSERTMSG 宏的代码包含在你的驱动程序中。

有关项目配置的详细信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

 

