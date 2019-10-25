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
ms.openlocfilehash: 9e8d65d605333c9f6ce08704f7042a2075165046
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836090"
---
# <a name="updating-wmi-registration-information"></a>更新 WMI 注册信息





使用 WMI 进行初始注册后，驱动程序通过使用以下操作之一调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)来更改其注册信息：

-   WMIREG\_操作\_重新注册，以将驱动程序先前提供的所有注册信息替换为新信息。

    作为响应，WMI 会将[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)请求或[**irp\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求发送到驱动程序 **，并将**设置为数据路径。 （在 Windows 98 和 Windows 2000 上，系统会发送**IRP\_MN\_REGINFO**请求。 在 Windows XP 和更高版本中，系统将**IRP\_MN\_REGINFO\_EX**请求。）

    该驱动程序为 WMI 提供其支持的所有块的新注册信息，如[使用 WMI 库注册块](using-the-wmi-library-to-register-blocks.md)和[处理 irp\_MN\_REGINFO 和 irp\_MN\_REGINFO\_EX注册块](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)。

-   WMIREG\_操作\_更新\_GUID，以便添加或删除块的支持或更改已注册块的静态实例名称。

    作为响应，WMI 会将[**irp\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或[**irp\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求发送到驱动程序，**并将**设置为数据路径。

    该驱动程序提供 WMI，其中包含更新的注册信息：

    -   驱动程序将 WMIREG\_标志设置为\_删除\_GUID，以删除对该块的支持。

    -   驱动程序将清除 WMIREG\_标记\_删除\_GUID，以添加新块或更新现有块。

    -   驱动程序将\_标志的 WMIREG 设置或清除\_实例\_*XXX* ，并提供任何必要的实例名称信息来更改块的静态实例名称或将其更改为使用动态实例名称。

-   WMIREG\_操作\_取消注册，以指示 WMI 驱动程序将不再提供 WMI 信息。

    WMI 不会发送**irp\_MN\_REGINFO**或**irp\_MN\_REGINFO\_EX**请求来响应此调用，因为它不需要驱动程序的详细信息。 驱动程序通常会注销其块响应[**IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)请求。 请注意，取消注册呼叫将会一直阻止，直到设备的所有 WMI Irp 完成。 如果驱动程序将 WMI Irp 排队，则必须在调用[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)之前将其取消。

 

 




