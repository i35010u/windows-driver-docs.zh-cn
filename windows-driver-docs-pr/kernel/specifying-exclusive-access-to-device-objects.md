---
title: 指定对设备对象的独占访问权限
description: 指定对设备对象的独占访问权限
ms.assetid: b492251b-55b0-4323-a508-b395bb3da0ef
keywords:
- 独占访问权 WDK 设备对象
- 设备对象 WDK 内核，独占访问权限
- 单一访问 WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb5fbe5f3a6e48105d951d2a93b5a56c5dad2f75
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533847"
---
# <a name="specifying-exclusive-access-to-device-objects"></a>指定对设备对象的独占访问权限





如果启用独占访问的设备，则一次可以打开到设备只有一个句柄。 要强制实施独占访问设备的 I/O 管理器，为独占属性必须设置为设备堆栈中的已命名的设备对象。

对于具有这两个 PDO WDM 设备堆栈和 FDO 独占属性仅可通过设置 INF 文件中，通过使用[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320)。 PDO 是在堆栈中的命名的对象，但总线驱动程序 （不是函数驱动程序本身） 创建 PDO，代表功能驱动程序。 指示要独占标志设置为 PDO 的总线驱动程序的唯一方式是由类或设备 INF 文件。 (在调用[ **IoCreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff548397)例程创建了 FDO; 独占标志设置为 FDO 不起作用。)

可以使用其设备对象不是堆积，如非 WDM 驱动程序和在原始模式下操作的设备驱动程序[ **IoCreateDeviceSecure** ](https://msdn.microsoft.com/library/windows/hardware/ff548407)例程，以将其命名的排他属性设置设备对象。

I/O 管理器强制实施独占性上指定的设备对象，而不考虑尾部的名称基于每个名称。 例如，假设设备对象具有名称"\\设备\\DeviceName"。 然后，I/O 管理器强制实施独占性请求以打开"\\设备\\DeviceName\\*Filename1*"后跟"\\设备\\DeviceName\\ *Filename2*"。 如果设备堆栈中的两个对象的命名 （这不推荐），I/O 管理器允许要打开的每个对象的一个句柄。 在这种情况下，驱动程序都必须强制实施独占性本身中其[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)回调函数。 I/O 管理器也不强制实施独占性相对于另一个文件句柄打开。 有关设备的命名空间中的文件打开请求的详细信息，请参阅[控制设备 Namespace 访问](controlling-device-namespace-access.md)。

 

 




