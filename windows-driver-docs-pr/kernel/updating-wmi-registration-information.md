---
title: 更新 WMI 注册信息
description: 更新 WMI 注册信息
ms.assetid: d24688e5-bb50-4bce-a4d4-4a3bf886f86d
keywords:
- WMI WDK 内核，用 WMI 注册
- 注册 WMI 数据提供程序
- 数据访问接口 WDK WMI
- 驱动程序注册 WDK WMI
- 事件块 WDK WMI
- 阻止 WDK WMI
- 注册块
- 正在更新 WMI 注册信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ffd2a9dbbb95f4f7ce557e1ad64ed54e4f27060
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187146"
---
# <a name="updating-wmi-registration-information"></a>更新 WMI 注册信息





使用 WMI 进行初始注册后，驱动程序通过使用以下操作之一调用 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol) 来更改其注册信息：

-   WMIREG \_ 操作重新 \_ 注册，以将驱动程序先前提供的所有注册信息替换为新信息。

    作为响应，WMI 会将 [**irp \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 请求或 [**irp \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求发送到驱动程序 **，并将** 设置为数据路径。  (在 Windows 98 和 Windows 2000 上，系统将发送 **IRP \_ MN \_ REGINFO** 请求。 在 Windows XP 和更高版本中，系统会发送 **IRP \_ MN \_ REGINFO \_ EX** 请求。 ) 

    该驱动程序为 WMI 提供其支持的所有块的新注册信息，如 [使用 WMI 库注册块](using-the-wmi-library-to-register-blocks.md) 和 [处理 irp \_ MN \_ REGINFO 和 Irp \_ MN \_ REGINFO \_ EX to register 块](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)中所述。

-   WMIREG \_ 操作 \_ 更新 \_ guid 以添加或删除对块的支持或更改已注册块的静态实例名称。

    作为响应，WMI 会将 [**irp \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 或 [**irp \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求发送到驱动程序， **并将** 设置为数据路径。

    该驱动程序提供 WMI，其中包含更新的注册信息：

    -   驱动程序将 WMIREG \_ 标志 \_ 删除 \_ GUID 设置为删除对该块的支持。

    -   驱动程序清除 WMIREG \_ 标志 \_ 删除 \_ GUID 以便添加新块或更新现有块。

    -   驱动程序设置或清除 WMIREG \_ 标志 \_ 实例 \_ *XXX* ，并提供任何必要的实例名称信息来更改块的静态实例名称或将其更改为使用动态实例名称。

-   WMIREG \_ 操作取消 \_ 注册以指示 wmi，驱动程序将不再提供 wmi 信息。

    WMI 不会发送 **irp \_ MN \_ REGINFO** 或 **irp \_ MN \_ REGINFO \_ EX** 请求来响应此调用，因为它不需要驱动程序的其他信息。 驱动程序通常会注销其块，以响应 [**IRP \_ MN \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求。 请注意，取消注册呼叫将会一直阻止，直到设备的所有 WMI Irp 完成。 如果驱动程序将 WMI Irp 排队，则必须在调用 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol) 之前将其取消。

 

