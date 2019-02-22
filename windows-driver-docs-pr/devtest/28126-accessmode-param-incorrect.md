---
title: C28126
description: ObReferenceObject * 警告 C28126 AccessMode 参数应为 irp->requestormode。
ms.assetid: be8f909e-2d4a-4e22-b457-81a048d90df8
keywords:
- 警告列出 WDK PREfast for Drivers
- 错误列出 WDK PREfast for Drivers
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28126
ms.openlocfilehash: b40ce9b2305c69628b90c9a8dc1664b84b58df3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547355"
---
# <a name="c28126"></a>C28126


警告 C28126:ObReferenceObject 的 AccessMode 参数\*应为 IRP-&gt;RequestorMode

在调用[ **ObReferenceObjectByHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff558679)或[ **ObReferenceObjectByPointer**](https://msdn.microsoft.com/library/windows/hardware/ff558686)，并传递该驱动程序**UserMode**或**KernelMode**有关*AccessMode*参数，而不是使用**Irp-&gt;RequestorMode**。

该驱动程序应使用**Irp-&gt;RequestorMode**，而不是指定**UserMode**或**KernelMode**。 这允许安全地提供内核模式句柄的内核模式 IRP 的发件人。

此警告适用于驱动程序堆栈中的顶级驱动程序。 可以忽略或禁止显示此警告对于所有其他驱动程序。

驱动程序堆栈中的顶级驱动程序应使用**Irp-&gt;RequestorMode**，而不是指定**UserMode**或**KernelMode**。 这允许安全地提供内核模式句柄的内核模式 IRP 的发件人。 堆栈中的所有其他驱动程序应指定**KernelMode**，以跳过的访问权限检查，并使负责访问权限检查到顶级的驱动程序。

 

 





