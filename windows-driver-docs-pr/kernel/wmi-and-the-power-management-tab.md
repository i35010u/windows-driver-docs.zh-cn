---
title: WMI 和电源管理选项卡
description: WMI 和电源管理选项卡
ms.assetid: ff270fc0-806b-4014-ba9c-9c321a10c893
keywords:
- WMI WDK 内核，属性表
- 属性表 WDK WMI
- 设备属性表 WDK WMI
- 电源管理 WDK WMI
- 属性页 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2045ef0e2cc8102c1876275cb7784bfa5620a631
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380930"
---
# <a name="wmi-and-the-power-management-tab"></a>WMI 和电源管理选项卡





支持电源管理的驱动程序可以自动启用**电源管理**设备属性表在设备管理器的选项卡。 如果驱动程序处理 GUID\_电源\_设备\_启用或 GUID\_POWER\_设备\_唤醒\_启用 WMI 类 Guid，设备管理器显示**电源管理**设备属性页上的选项卡。 某些控件的属性页上启用具体取决于哪个 WMI 类 Guid 的驱动程序支持。

GUID\_电源\_设备\_*XXX*类 Guid 启用控件的属性页上，如下所示：

-   GUID\_POWER\_DEVICE\_ENABLE

    启用一个复选框以激活或停用设备的电源管理。 WMI 类的数据块包含单个布尔值，该值指示是否启用电源管理。 值的含义与设备相关。

-   GUID\_POWER\_DEVICE\_WAKE\_ENABLE

    启用一个复选框以激活或停用发送等待/唤醒 Irp。 选中时，驱动程序应发送[ **IRP\_MN\_等待\_唤醒**](https://msdn.microsoft.com/library/windows/hardware/ff551766)请求到其物理设备对象。 这可让设备唤醒系统以响应外部事件。 例如，如果启用了键盘类驱动程序，键盘设备将唤醒系统时按下某个键。 如果不选中复选框，该驱动程序应取消**IRP\_MN\_等待\_唤醒**请求。 WMI 类的数据块包含单个布尔值，该值指示复选框的当前状态。

WMI 查询请求的 guid 发送\_电源\_设备\_*XXX* WMI 类时，只要该驱动程序的属性表打开设备管理器中的 Guid。 WMI 更改请求时对值的复选框之一发送**电源管理**选项卡上的更改。 用户希望他们设置保持一致驱动程序加载和卸载，因此驱动程序应将这两个属性的当前值存储在注册表中的值。

鼠标或键盘类示例驱动程序这两个处理 GUID\_电源\_设备\_唤醒\_启用 WMI 类的 GUID。 请参阅\\src\\输入\\kbdclass 和\\src\\输入\\mouclass Windows Driver Kit (WDK) 中。

 

 




