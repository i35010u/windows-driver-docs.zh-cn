---
title: 中断到调试器从 KMDF 驱动程序
description: 中断到调试器从 KMDF 驱动程序
ms.assetid: b18e210c-cc9b-436c-b762-6346b946357c
keywords:
- 调试驱动程序 WDK KMDF，中断到调试器
- 中断到调试器 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7afbfcffa7b84d9464fbe292a193653e3597d9c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525497"
---
# <a name="breaking-into-a-debugger-from-kmdf-drivers"></a>中断到调试器从 KMDF 驱动程序


如果您希望基于 framework 的驱动程序以在内核模式调试器中中断，可以使用以下：

-   [ **WdfVerifierDbgBreakPoint** ](https://msdn.microsoft.com/library/windows/hardware/ff551164)函数会中断到调试器，如果[DbgBreakOnError](registry-values-for-debugging-kmdf-drivers.md)在注册表中设置值。

-   [ **WDFVERIFY** ](https://msdn.microsoft.com/library/windows/hardware/ff551167)宏测试的逻辑表达式，并强行进入内核调试器，如果表达式的计算结果**FALSE**如果[VerifyOn](registry-values-for-debugging-kmdf-drivers.md)在注册表中设置值。

-   [**验证\_IS\_IRQL\_被动\_级别**](https://msdn.microsoft.com/library/windows/hardware/ff545588)宏进入内核调试器如果驱动程序不执行在 IRQL = 被动\_级别; 如果**VerifyOn**在注册表中设置值。

-   [ **ASSERT** ](https://msdn.microsoft.com/library/windows/hardware/ff542107)宏测试的逻辑表达式，并强行进入内核调试器，如果表达式的计算结果**FALSE**。

-   [ **ASSERTMSG** ](https://msdn.microsoft.com/library/windows/hardware/ff542113)宏测试表达式和表达式的计算结果**FALSE**、 进入内核调试器，并提供可显示的短信向调试器。

-   [ **DbgPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff543634)并[ **KdPrintEx** ](https://msdn.microsoft.com/library/windows/hardware/ff548100)函数都提供可显示的短信向调试器。

WDFVERIFY 和验证代码\_IS\_IRQL\_被动\_级别宏包含在您的驱动程序时生成您的版本或调试配置中的驱动程序 (称为免费构建环境或已检验的版本环境在 Windows 7 及更早版本）。 仅当您构建您的驱动程序中的调试配置时，驱动程序中包含的断言和 ASSERTMSG 宏代码。

有关项目配置的详细信息，请参阅[构建一个驱动程序](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)。

 

 





