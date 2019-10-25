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
ms.openlocfilehash: 3fb20e1e13db1882fb3d9e85290b887541d49045
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845508"
---
# <a name="bug-checks-from-kmdf-drivers"></a>从 KMDF 驱动程序进行 Bug 检查


框架检查基于框架的驱动程序中的几种类型的错误。 如果发生这些错误之一，则该框架会创建 WDF\_冲突 bug 检查。

有关框架所检查的驱动程序错误的类型的信息，请参阅[**WDF\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x10d---wdf-violation)。

你的驱动程序可以通过调用[**WdfVerifierKeBugCheck**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfverifier/nf-wdfverifier-wdfverifierkebugcheck)来创建 bug 检查。

 

 





