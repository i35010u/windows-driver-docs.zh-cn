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
ms.openlocfilehash: 7ea1a1387117ba1509030fb1fbb7fe13bd6de88e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353206"
---
# <a name="bug-checks-from-kmdf-drivers"></a>从 KMDF 驱动程序进行 Bug 检查


该框架会为多种类型的基于框架的驱动程序中的错误。 如果发生这些错误之一，则框架将创建 WDF\_冲突错误检查。

有关该框架会为驱动程序错误类型的信息，请参阅[ **WDF\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)。

您的驱动程序可以通过调用创建的 bug 检查[ **WdfVerifierKeBugCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfverifier/nf-wdfverifier-wdfverifierkebugcheck)。

 

 





