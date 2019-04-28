---
title: 删除中断对象
description: 删除中断对象
ms.assetid: B72DA452-B22F-47CD-8C5D-E741F09F556E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7432fb4727fe0460b3ecfa3eaff927e1c7e1449c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330879"
---
# <a name="deleting-an-interrupt-object"></a>删除中断对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

如果该驱动程序创建一个中断对象通过调用[ **IWDFDevice3::CreateInterrupt**](https://msdn.microsoft.com/library/windows/hardware/hh451208)，驱动程序不需要删除中断对象。 因为中断对象是 framework 设备对象的子对象，该框架将自动删除中断对象。

框架使用以下规则：

-   如果该驱动程序调用[ **CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)从其[ **OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)回调方法，该框架中删除中断对象后从驱动程序将返回其[ **OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439739)回调。

-   如果该驱动程序调用[ **CreateInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/hh451208)从其[ **OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)回调方法，该框架中删除中断对象删除设备时。

（可选） 该驱动程序可以调用[ **IWDFObject::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)在任何时候删除的中断对象。 因为驱动程序不能创建新的中断对象之外[ **OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)或[ **OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/hh439734)，手动删除的除非驱动程序必须删除对象，该框架将其删除之前，不应使用对象。

 

 





