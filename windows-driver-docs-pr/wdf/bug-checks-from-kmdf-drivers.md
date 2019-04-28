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
ms.openlocfilehash: 776ea4eb7b2135b7599e0a657a8084c8447236f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330859"
---
# <a name="bug-checks-from-kmdf-drivers"></a>从 KMDF 驱动程序进行 Bug 检查


该框架会为多种类型的基于框架的驱动程序中的错误。 如果发生这些错误之一，则框架将创建 WDF\_冲突错误检查。

有关该框架会为驱动程序错误类型的信息，请参阅[ **WDF\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff557235)。

您的驱动程序可以通过调用创建的 bug 检查[ **WdfVerifierKeBugCheck**](https://msdn.microsoft.com/library/windows/hardware/ff551166)。

 

 





