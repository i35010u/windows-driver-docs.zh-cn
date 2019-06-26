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
ms.openlocfilehash: 2e8f5a25e1df4d68e3d94907111e327dbafeeb7f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373471"
---
# <a name="registering-as-a-wmi-data-provider"></a>注册为 WMI 数据提供程序





支持 WMI 的驱动程序必须将注册为 WMI 数据提供程序，以使其数据和事件块可向 WMI 客户端。 设备驱动程序可以处理 WMI Irp 的点到初始化后启动其设备时，驱动程序通常向 WMI 中进行注册。 在注册过程中，该驱动程序 WMI 将指针传递到其设备对象和它支持的数据和事件块有关的信息。

驱动程序向 WMI 注册两个阶段：

1.  驱动程序调用[ **IoWMIRegistrationControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)与操作 WMIREG\_操作\_注册和设备对象的指针传递给驱动程序的[*AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。

2.  驱动程序句柄[ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或者[ **IRP\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex) WMI 驱动程序的响应中发送的请求**IoWMIRegistrationControl**调用。 **Parameters.WMI.DataPath** IRP 的成员设置为 WMIREGISTER 和**Parameters.WMI.ProviderId**设置为驱动程序的设备对象指针。 驱动程序提供有关其数据和事件的块，通过使用 WMI 库中所述的注册信息的 WMI[使用 WMI 库对注册块](using-the-wmi-library-to-register-blocks.md)，或通过处理**IRP\_MN\_REGINFO**或**IRP\_MN\_REGINFO\_EX**请求中所述[处理 IRP\_MN\_REGINFO 和 IRP\_MN\_REGINFO\_EX 注册块](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)。

 

 




