---
title: 注册为 WMI 数据提供程序
description: 注册为 WMI 数据提供程序
ms.assetid: a08fed24-20b6-46aa-9a52-7a22f0e89ce4
keywords:
- WMI WDK 内核，向 WMI 注册
- 注册 WMI 数据提供程序
- 数据提供程序 WDK WMI
- 驱动程序注册 WDK WMI
- 事件阻止 WDK WMI
- 块 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc3f118d480c59ac997f4afaf0221a6abe1094ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523176"
---
# <a name="registering-as-a-wmi-data-provider"></a>注册为 WMI 数据提供程序





支持 WMI 的驱动程序必须将注册为 WMI 数据提供程序，以使其数据和事件块可向 WMI 客户端。 设备驱动程序可以处理 WMI Irp 的点到初始化后启动其设备时，驱动程序通常向 WMI 中进行注册。 在注册过程中，该驱动程序 WMI 将指针传递到其设备对象和它支持的数据和事件块有关的信息。

驱动程序向 WMI 注册两个阶段：

1.  驱动程序调用[ **IoWMIRegistrationControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550480)与操作 WMIREG\_操作\_注册和设备对象的指针传递给驱动程序的[*AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。

2.  驱动程序句柄[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)或者[ **IRP\_MN\_REGINFO\_EX**](https://msdn.microsoft.com/library/windows/hardware/ff551734) WMI 驱动程序的响应中发送的请求**IoWMIRegistrationControl**调用。 **Parameters.WMI.DataPath** IRP 的成员设置为 WMIREGISTER 和**Parameters.WMI.ProviderId**设置为驱动程序的设备对象指针。 驱动程序提供有关其数据和事件的块，通过使用 WMI 库中所述的注册信息的 WMI[使用 WMI 库对注册块](using-the-wmi-library-to-register-blocks.md)，或通过处理**IRP\_MN\_REGINFO**或**IRP\_MN\_REGINFO\_EX**请求中所述[处理 IRP\_MN\_REGINFO 和 IRP\_MN\_REGINFO\_EX 注册块](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)。

 

 




