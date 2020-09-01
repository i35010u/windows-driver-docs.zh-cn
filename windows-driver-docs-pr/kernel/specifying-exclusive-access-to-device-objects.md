---
title: 指定对设备对象的独占访问权限
description: 指定对设备对象的独占访问权限
ms.assetid: b492251b-55b0-4323-a508-b395bb3da0ef
keywords:
- 独占访问 WDK 设备对象
- 设备对象 WDK 内核，独占访问
- 单个 access WDK 设备对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 914d733669a593b58a99e2bb21a4ed6cbf0b3b63
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187873"
---
# <a name="specifying-exclusive-access-to-device-objects"></a>指定对设备对象的独占访问权限





如果启用了对设备的独占访问，则一次只能打开设备的一个句柄。 要使 i/o 管理器强制对设备进行独占访问，必须为设备堆栈中的命名设备对象设置独占属性。

对于具有 PDO 和 FDO 的 WDM 设备堆栈，专用属性只能由 INF 文件使用 [**Inf AddReg 指令**](../install/inf-addreg-directive.md)来设置。 PDO 是堆栈中的命名对象，但总线驱动程序 (功能驱动程序本身，) 会代表函数驱动程序创建 PDO。 指示总线驱动程序为 PDO 设置独占标志的唯一方法是使用类或设备 INF 文件。  (调用 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 例程会创建 FDO;设置 FDO 的独占标志不起作用。 ) 

如果驱动程序的设备对象不是堆叠的，例如非 WDM 驱动程序和在 raw 模式下运行的设备，则可以使用 [**IoCreateDeviceSecure**](/windows-hardware/drivers/ddi/wdmsec/nf-wdmsec-wdmlibiocreatedevicesecure) 例程为其命名设备对象设置独占属性。

每个命名设备对象上的独占性根据每个名称强制执行，而不考虑尾随名称。 例如，假设设备对象的名称为 " \\ device \\ DeviceName"。 然后，i/o 管理器强制独占性请求打开 " \\ device \\ DeviceName \\ *Filename1*"，后跟 " \\ device \\ DeviceName \\ *Filename2*"。 如果设备堆栈中的两个对象都命名 (这是不建议的) ，则 i/o 管理器允许为每个对象打开一个句柄。 在这种情况下，驱动程序必须在其 [*DRIVER_DISPATCH*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 回调函数中强制执行独占性。 I/o 管理器还不强制独占性相对于其他文件句柄打开。 有关设备命名空间中的文件打开请求的详细信息，请参阅 [控制设备命名空间访问](controlling-device-namespace-access.md)。

 

