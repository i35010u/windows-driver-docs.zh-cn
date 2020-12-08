---
title: 从 KMDF 驱动程序进行 Bug 检查
description: 从 KMDF 驱动程序进行 Bug 检查
keywords:
- 调试驱动程序 WDK KMDF，bug 检查
- bug 检查 WDK KMDF
- 验证 KMDF 代码
- KMDF bug 检查 WDK
- WDF_VIOLATION
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d48ff9eebc898a2341c8268c244659ff257c715c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815783"
---
# <a name="bug-checks-from-kmdf-drivers"></a>从 KMDF 驱动程序进行 Bug 检查


框架检查基于框架的驱动程序中的几种类型的错误。 如果发生这些错误之一，则该框架会创建 WDF \_ 冲突 bug 检查。

有关框架所检查的驱动程序错误的类型的信息，请参阅 [**WDF \_ 冲突**](../debugger/bug-check-0x10d---wdf-violation.md)。

你的驱动程序可以通过调用 [**WdfVerifierKeBugCheck**](/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierkebugcheck)来创建 bug 检查。

 

