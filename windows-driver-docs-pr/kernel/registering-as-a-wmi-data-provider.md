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
ms.openlocfilehash: ef0ed280b0a0307fd6469dd3990332e88966337b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190445"
---
# <a name="registering-as-a-wmi-data-provider"></a>注册为 WMI 数据提供程序





支持 WMI 的驱动程序必须注册为 WMI 数据提供程序，以使其数据和事件块可供 WMI 客户端使用。 驱动程序在启动其设备时，通常会向 WMI 注册，然后将设备初始化为驱动程序可以处理 WMI Irp 的点。 在注册过程中，驱动程序会向 WMI 传递一个指向其设备对象的指针以及它所支持的数据和事件块的相关信息。

驱动程序在两个阶段中注册 WMI：

1.  驱动程序调用 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol) ，其中包含操作 WMIREG \_ 操作 \_ 注册，以及一个指向传递给驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程的设备对象的指针。

2.  驱动程序将处理 [**irp \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 或 [**irp \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求，WMI 会发送该请求来响应驱动程序的 **IoWMIRegistrationControl** 调用。 IRP 的 **数据路径** 成员设置为 WMIREGISTER **，并将** 设置为驱动程序的设备对象指针。 该驱动程序通过使用 wmi 库中所述的有关数据和事件块的注册信息向 WMI 提供注册[块，如使用 Wmi 库注册块](using-the-wmi-library-to-register-blocks.md)中所述，或处理**irp \_ MN \_ REGINFO**或**irp \_ MN \_ REGINFO \_ ex** [请求。 \_ \_ \_ \_ \_ ](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)

 

