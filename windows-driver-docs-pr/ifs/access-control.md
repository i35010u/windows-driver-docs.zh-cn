---
title: 访问控制
description: 访问控制
ms.assetid: 7f87276f-4014-4b37-b051-4bf02acbf575
keywords:
- 安全 WDK 文件系统、 最大程度减少威胁
- 访问控制 WDK 文件系统
- 访问验证 WDK 文件系统
- 验证安全 WDK 文件系统
- 检查安全性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00ad6d5df9d0f2555f85800231a8af85eb4268c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323143"
---
# <a name="access-control"></a>访问控制


## <span id="ddk_access_control_if"></span><span id="DDK_ACCESS_CONTROL_IF"></span>


保护自身免遭不适当的访问，大多数驱动程序依赖于由已对其设备的对象的 I/O 管理器应用的默认访问控制。 其他机制可供驱动程序。 或许最简单的正常的驱动程序是将显式安全描述符应用在安装其驱动程序时。 将安全描述符应用到的设备对象的示例将在后面的部分讨论。

实现自己的安全策略的驱动程序可能依赖于用于协助管理的安全访问的标准 Windows Api。 在这种情况下，驱动程序管理的安全描述符的存储，并负责调用安全引用监视器例程来验证安全。 其中包括许多例程，如下所示：

-   [**SeAccessCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563674)-此例程比较对调用方的安全凭据的安全描述符。

-   [**SePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff556686)-此例程确定调用方是否启用给定的权限。

-   [**SeSinglePrivilegeCheck**](https://msdn.microsoft.com/library/windows/hardware/ff563740)-此例程确定是否为调用方启用了特定权限。

-   [**SeAuditingFileOrGlobalEvents**](https://msdn.microsoft.com/library/windows/hardware/ff554778)-此例程指示系统是否已启用审核。

-   [**SeOpenObjectAuditAlarm**](https://msdn.microsoft.com/library/windows/hardware/ff556682)-此例程审核打开的对象事件。

此列表不完整，但它描述了多个可以在一个驱动程序用于执行访问验证关键功能。

 

 




