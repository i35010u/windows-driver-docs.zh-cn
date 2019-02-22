---
title: Framework I/O 目标对象
description: Framework I/O 目标对象
ms.assetid: 355a1818-88c9-4989-9141-8445f511f501
keywords:
- UMDF 对象 WDK，I/O 的目标对象
- framework 对象 WDK UMDF，I/O 目标对象
- I/O 目标对象 WDK UMDF
- IWDFIoTarget
- 针对 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c2861dea511b6e8c975c12861285a0ca8567c60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546249"
---
# <a name="framework-io-target-object"></a>Framework I/O 目标对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

向驱动程序通过公开 framework I/O 目标对象[IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170)接口。 它检索的 I/O 目标，通常表示堆栈中的较低的驱动程序有关的信息，但也可以表示另一个 UMDF 驱动程序或堆栈的内核模式部分。 I/O 目标对象提供 UMDF 驱动程序将请求发送到另一台设备的方法。

此外可以使用 UMDF 驱动程序[IWDFIoTargetStateManagement](https://msdn.microsoft.com/library/windows/hardware/ff559198)界面来管理和监视 I/O 目标对象的状态。

 

 





