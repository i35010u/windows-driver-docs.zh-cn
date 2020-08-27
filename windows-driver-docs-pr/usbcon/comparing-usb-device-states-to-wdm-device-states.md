---
description: 本主题介绍通用串行总线2.0 规范的9.1 节中指定的 USB 设备电源状态所使用的 WDM 设备状态。
title: USB 设备电源状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f423881c44846aa1e709260d8907ec69f1e148e7
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968518"
---
# <a name="usb-device-power-states"></a>USB 设备电源状态


本主题介绍通用串行总线2.0 规范的9.1 节中指定的 USB 设备电源状态所使用的 WDM 设备状态。

USB 设备电源状态 (通用串行总线 2.0) 规范的9.1 节中指定的，可分为三个常规类别：

-   已连接：设备已连接，但未完全接通电源。
-   已通电：设备处于完全供电状态之一： "默认"、"地址" 或 "已配置"。
-   已挂起：设备处于空闲状态，并且在低功耗状态下运行。

在 WDM 电源模式中定义的设备电源状态与 USB 标准中定义的设备电源状态之间没有直接的关联。 例如，"已 *暂停* " 和 " *空闲* " 条款在 USB 规范中具有特别意义;但这些术语通常在 WDM 电源模型中使用方式不同。 Windows 客户端驱动程序可以使 USB 设备处于挂起状态。 有关详细信息，请参阅 [USB 选择性挂起](usb-selective-suspend.md)。 当客户端驱动程序准备好挂起其设备时，它将指示总线驱动程序将其空闲。 有关空闲请求的讨论，请参阅 [USB 选择性挂起](usb-selective-suspend.md)。

WDM 模型中的设备电源状态可以总结如下：

-   **D0** -工作状态。 设备已完全接通电源。
-   **D1/D2** -中间睡眠状态。 这些状态允许设备用于远程唤醒。
-   **D3** -最深层睡眠状态。 状态 **D3** 中的设备无法用于远程唤醒。

有关 WDM 电源模式下设备电源状态的完整讨论，请参阅 [设备电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)。

WDM 电源模式使用设备的术语 " *武装* " 进行远程唤醒。 武装是通常（但不总是）会导致硬件操作在 USB 设备上 *启用* 远程唤醒功能的软件操作。 用于远程唤醒设备的 WDM 软件操作是等待唤醒 IRP ([**IRP \_ MN \_ 等待 \_ 唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) 。 有关此 IRP 的详细信息，请参阅 [支持具有唤醒功能的设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)。

有关此软件操作与启用 USB 远程唤醒功能之间的关系的说明，请参阅 [远程唤醒 Usb 设备](remote-wakeup-of-usb-devices.md)。

此节包含以下子节：

-   [更改非复合设备的电源状态](#changing-the-power-state-of-a-non-composite-device)
-   [更改复合设备的电源状态](#changing-the-power-state-of-a-composite-device)
-   [相关主题](#related-topics)

## <a name="changing-the-power-state-of-a-non-composite-device"></a>更改非复合设备的电源状态


USB 设备的电源策略管理器负责设置设备的电源状态。 电源策略管理器通过发出 WDM power ([**irp \_ MN \_ 设置 \_ power**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) irp 来设置电源状态。 有关电源策略管理器的详细信息，请参阅 [电源策略所有权](https://docs.microsoft.com/windows-hardware/drivers/wdf/power-policy-ownership)。

总线驱动程序执行的操作取决于电源策略管理器请求的设备电源级别。 下面列出了总线驱动程序为每个级别的设置电源请求所执行的操作：

-   **D0**

    总线驱动程序执行以下任务：

    1.  确保所有 upsteam USB 集线器都已准备就绪，可以接收请求。
    2.  \_如果设备的 USB 端口处于挂起状态，则通过清除端口挂起功能来恢复端口。
    3.  如果一个处于挂起状态，则完成设备的空闲 IRP，状态为 \_ "成功"。
    4.  如果设备已配备，请 Disarm 该设备的远程唤醒。
-   **D1/D2**

    总线驱动程序执行以下任务：

    1.  如果等待唤醒 IRP ([**IRP \_ MN \_ wait \_ 唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) 处于挂起状态，则设备用于远程唤醒。
    2.  通过设置端口挂起功能挂起设备的 USB 端口 \_ 。
-   **D3**

    总线驱动程序执行以下任务：

    1.  通过设置端口挂起功能挂起设备的 USB 端口 \_ 。
    2.  完成设备的等待唤醒 IRP \_ \_ ，状态为 "电源状态 \_ 无效" （如果有）。
    3.  完成设备的空闲 IRP ([**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 状态为 \_ "电源 \_ 状态 \_ 无效，如果一个处于挂起状态。

## <a name="changing-the-power-state-of-a-composite-device"></a>更改复合设备的电源状态


复合设备上某个接口的客户端驱动程序必须与设备上其他接口的客户端驱动程序共享复合设备的电源状态。 因此，接口的客户端驱动程序无法将复合设备置于低功耗状态，并且不会影响设备上的其他接口。 当接口的客户端驱动程序发送[**IRP \_ MN \_ 设置 \_ 电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求时， [USB 泛型父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md)会执行以下操作。

-   **D0**

    总线驱动程序执行以下任务：

    1.  确保所有 upsteam USB 集线器都已准备就绪，可以接收请求。
    2.  \_如果设备的 USB 端口处于挂起状态，则通过清除端口挂起功能来恢复端口。
    3.  如果一个处于挂起状态，则完成客户端驱动程序的空闲 IRP，状态为 \_ "成功"。
-   **D1/D2**

    总线驱动程序不执行任何操作。

-   **D3**

    总线驱动程序执行以下任务：

    1.  完成客户端驱动程序的等待唤醒 IRP (IRP \_ MN \_ 等待 \_ 唤醒) ，其状态 \_ \_ 为 "电源状态 \_ 无效，如果一个处于挂起状态。
    2.  完成客户端驱动程序的空闲 IRP ([**IOCTL \_ 内部 \_ USB \_ 提交 \_ 空闲 \_ 通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) \_ \_ \_ 如果一个处于挂起状态，则状态电源状态无效。

如果满足以下条件之一，一般父驱动程序会挂起设备的 USB 端口：

-   系统正在转换为低功耗状态。
-   复合设备上所有函数的客户端驱动程序启动了选择性挂起。

## <a name="related-topics"></a>相关主题
[USB 电源管理](usb-power-management.md)  



