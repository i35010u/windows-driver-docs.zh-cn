---
title: WMI 和电源管理选项卡
description: WMI 和电源管理选项卡
keywords:
- WMI WDK 内核，属性表
- 属性表 WDK WMI
- 设备属性表 WDK WMI
- 电源管理 WDK WMI
- 属性页 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae3f60261074a5bc3ddd95b52797dcd76ef80bf9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782695"
---
# <a name="wmi-and-the-power-management-tab"></a>WMI 和电源管理选项卡





支持电源管理的驱动程序可以在设备管理器中自动启用设备属性表的 " **电源管理** " 选项卡。 如果驱动程序处理 GUID \_ power \_ device \_ enable 或 guid \_ POWER \_ Device \_ 唤醒 \_ enable WMI class guid，设备管理器将在设备属性表中显示一个 **电源管理** 选项卡。 根据驱动程序支持的 WMI 类 Guid，启用属性页上的某些控件。

GUID \_ 电源 \_ 设备 \_ *XXX* 类 guid 在属性页上启用控件，如下所示：

-   GUID \_ 电源 \_ 设备 \_ 启用

    启用一个复选框，以激活或停用设备的电源管理。 WMI 类的数据块包含一个布尔值，该值指示是否启用电源管理。 值的含义与设备相关。

    > [!NOTE]
    > 通常不建议用户在新式备用系统上修改这些设置，因为这可能会导致电池电量大幅降低。

-   GUID \_ POWER \_ DEVICE \_ 唤醒 \_ 启用

    启用一个复选框，以激活或停用发送等待/唤醒 Irp。 如果选择此选项，驱动程序应将 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) 请求发送到其物理设备对象。 这使设备可以唤醒系统以响应外部事件。 此设置通常不会影响设备从新式备用设备唤醒系统的能力，而不会影响低功耗系统状态 (Sx，其中 x > 0) 。 例如，为键盘类驱动程序启用时，键盘设备会在按下某个键时唤醒系统。 如果未选中该复选框，则驱动程序应取消 **IRP \_ MN \_ WAIT \_ 唤醒** 请求。 WMI 类的数据块包含一个布尔值，该值指示复选框的当前状态。

\_ \_ \_ 每当在设备管理器中打开驱动程序的属性表时，都会为 GUID POWER DEVICE *XXX* wmi 类 guid 发送 wmi 查询请求。 只要 " **电源管理** " 选项卡上的一个复选框值发生更改，就会发送 WMI 更改请求。 用户将希望其设置的值在驱动程序加载和卸载之间保持不变，因此驱动程序应将其中任一属性的当前值存储在注册表中。

鼠标或键盘类示例驱动程序都处理 GUID \_ POWER \_ DEVICE \_ 唤醒 \_ ENABLE WMI class guid。 请 \\ 参阅 \\ \\ \\ \\ \\ Windows 驱动程序工具包中的 src input KBDCLASS 和 src input mouclass (WDK) 。

