---
title: 从 KMDF 驱动程序进行 Bug 检查
description: 从 KMDF 驱动程序进行 Bug 检查
ms.assetid: 4fde9586-3455-4692-8eeb-bbf64c0a437e
keywords:
- 调试驱动程序 WDK KMDF，bug 检查
- bug 检查 WDK KMDF
- 验证 KMDF 代码
- KMDF bug 检查 WDK
- WDF_VIOLATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36c5b3701e67fdb2a5df082d2d9450c5b10c01fd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184049"
---
# <a name="bug-checks-from-kmdf-drivers"></a>从 KMDF 驱动程序进行 Bug 检查


框架检查基于框架的驱动程序中的几种类型的错误。 如果发生这些错误之一，则该框架会创建 WDF \_ 冲突 bug 检查。

有关框架所检查的驱动程序错误的类型的信息，请参阅 [**WDF \_ 冲突**](../debugger/bug-check-0x10d---wdf-violation.md)。

你的驱动程序可以通过调用 [**WdfVerifierKeBugCheck**](/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierkebugcheck)来创建 bug 检查。

 

