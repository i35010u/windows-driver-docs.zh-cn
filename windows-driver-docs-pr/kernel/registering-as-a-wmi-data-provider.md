---
title: 注册为 WMI 数据提供程序
description: 注册为 WMI 数据提供程序
ms.assetid: a08fed24-20b6-46aa-9a52-7a22f0e89ce4
keywords:
- WMI WDK 内核，用 WMI 注册
- 注册 WMI 数据提供程序
- 数据访问接口 WDK WMI
- 驱动程序注册 WDK WMI
- 事件块 WDK WMI
- 阻止 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f128523fc91a06c62d7f7159a8a66e879eeda642
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838468"
---
# <a name="registering-as-a-wmi-data-provider"></a>注册为 WMI 数据提供程序





支持 WMI 的驱动程序必须注册为 WMI 数据提供程序，以使其数据和事件块可供 WMI 客户端使用。 驱动程序在启动其设备时，通常会向 WMI 注册，然后将设备初始化为驱动程序可以处理 WMI Irp 的点。 在注册过程中，驱动程序会向 WMI 传递一个指向其设备对象的指针以及它所支持的数据和事件块的相关信息。

驱动程序在两个阶段中注册 WMI：

1.  驱动程序调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol) ，其中包含 action WMIREG\_操作\_REGISTER，并向传递到驱动程序的[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的设备对象发送指针。

2.  该驱动程序处理[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或[**irp\_MN\_\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex) ，因为 WMI 发送此请求是为了响应驱动程序的**IoWMIRegistrationControl**调用。 IRP 的**数据路径**成员设置为 WMIREGISTER **，并将**设置为驱动程序的设备对象指针。 该驱动程序通过使用 wmi 库中所述的有关数据和事件块的注册信息向 WMI 提供注册[块，如使用 Wmi 库注册块](using-the-wmi-library-to-register-blocks.md)或处理**irp\_MN\_REGINFO**或**irp\_MN\_REGINFO\_EX**请求，如[处理 IRP\_MN\_REGINFO 和 IRP\_MN\_REGINFO\_Ex 到 Register 块](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)。

 

 




