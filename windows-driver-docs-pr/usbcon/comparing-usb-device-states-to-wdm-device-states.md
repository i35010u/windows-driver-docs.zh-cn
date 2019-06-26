---
Description: 本主题介绍了要使用 USB 设备电源状态为指定的通用串行总线 2.0 规范的 9.1 节中的 WDM 设备状态。
title: USB 设备电源状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58ab116a5397dd9a151334fddd392f6f58d2f836
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381111"
---
# <a name="usb-device-power-states"></a>USB 设备电源状态


本主题介绍了要使用 USB 设备电源状态为指定的通用串行总线 2.0 规范的 9.1 节中的 WDM 设备状态。

（在通用串行总线 2.0 规范的 9.1 节中指定） 的 USB 设备的电源状态可分为三个常规类别：

-   附件：附加，但不是完全支持的设备。
-   提供支持：在设备处于正常通电状态之一：默认值、 解决问题，或配置。
-   挂起：设备处于空闲状态且低电源。

WDM power 模型中定义的设备电源状态和 USB 标准中定义的设备电源状态之间没有直接关联。 例如，术语*挂起*和*空闲*在 USB 中具有非常特定的含义规范; 但是这些术语通常以不同的方式中使用 WDM 电源模型。 Windows 客户端驱动程序可以将 USB 设备置于 Suspended 状态。 有关详细信息，请参阅[USB 选择性挂起](usb-selective-suspend.md)。 准备就绪，若要挂起其设备的客户端驱动程序时，它指示空闲状态，则总线驱动程序。 空闲状态请求的讨论，请参阅[USB 选择性挂起](usb-selective-suspend.md)。

WDM 模型中的设备的电源状态可以总结如下：

-   **D0** -工作状态。 完全打开设备。
-   **D1/D2** -中间睡眠状态。 这些状态允许设备后，若要了解有关远程唤醒。
-   **D3** -最深的睡眠状态。 状态中的设备**D3**不能有用于远程唤醒。

WDM power 模型中的设备的电源状态的完整讨论，请参阅[设备的电源状态](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-power-states)。

WDM 电源模型使用术语*武装*的远程唤醒设备。 武装是软件的操作，通常情况下，但不是总是会导致的硬件操作*启用*USB 设备上的远程唤醒功能。 而远程唤醒的设备的 WDM 软件操作是等待唤醒 IRP ([**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake))。 有关此 IRP 的详细信息，请参阅[支持设备的已唤醒功能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)。

有关此软件操作和启用该 USB 远程唤醒功能之间的关系的说明，请参阅[USB 设备的远程唤醒](remote-wakeup-of-usb-devices.md)。

本部分包含以下子部分：

-   [更改的非复合设备的电源状态](#changing-the-power-state-of-a-non-composite-device)
-   [更改复合设备的电源状态](#changing-the-power-state-of-a-composite-device)
-   [相关主题](#related-topics)

## <a name="changing-the-power-state-of-a-non-composite-device"></a>更改的非复合设备的电源状态


USB 设备的电源策略管理器负责设置设备的电源状态。 电源策略管理器通过发出 WDM 电源设置的电源状态 ([**IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)) IRP。 有关电源策略管理器的详细信息，请参阅[电源策略所有权](https://docs.microsoft.com/windows-hardware/drivers/wdf/power-policy-ownership)。

总线驱动程序所采取的操作取决于电源策略管理器请求的设备电源级别。 下面列出了为每个级别集 power 请求总线驱动程序所执行的操作：

-   **D0**

    总线驱动程序将执行以下任务：

    1.  确保所有 upsteam USB 集线器都都加电并准备好接收请求。
    2.  通过清除端口恢复端口\_挂起功能，如果挂起设备的 USB 端口。
    3.  完成设备的状态为空闲 IRP\_成功后，如果其中一个处于挂起状态。
    4.  如果已有，请清除远程唤醒设备。
-   **D1/D2**

    总线驱动程序将执行以下任务：

    1.  如果等待唤醒 IRP 而远程唤醒设备 ([**IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)) 处于挂起状态。
    2.  通过设置端口挂起设备的 USB 端口\_挂起功能。
-   **D3**

    总线驱动程序将执行以下任务：

    1.  通过设置端口挂起设备的 USB 端口\_挂起功能。
    2.  完成设备的等待唤醒状态的 IRP\_电源\_状态\_无效，如果其中一个处于挂起状态。
    3.  完成设备的空闲 IRP ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 状态\_POWER\_状态\_无效，如果其中一个处于挂起状态。

## <a name="changing-the-power-state-of-a-composite-device"></a>更改复合设备的电源状态


复合设备上某个接口的客户端驱动程序必须与在设备上的其他接口的客户端驱动程序共享复合设备电源的状态。 因此接口的客户端驱动程序不能将复合设备置于低功率状态而不会影响设备上的其他接口。 [USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)接口的客户端驱动程序发送时采取以下措施[ **IRP\_MN\_设置\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求。

-   **D0**

    总线驱动程序将执行以下任务：

    1.  确保所有 upsteam USB 集线器都都加电并准备好接收请求。
    2.  通过清除端口恢复端口\_挂起功能，如果挂起设备的 USB 端口。
    3.  完成客户端驱动程序的空闲状态与 IRP\_成功后，如果其中一个处于挂起状态。
-   **D1/D2**

    总线驱动程序不执行任何操作。

-   **D3**

    总线驱动程序将执行以下任务：

    1.  完成客户端驱动程序等待唤醒 IRP (IRP\_MN\_等待\_唤醒) 状态\_POWER\_状态\_无效，如果其中一个处于挂起状态。
    2.  完成客户端驱动程序的空闲 IRP ([**IOCTL\_内部\_USB\_提交\_空闲\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_idle_notification)) 状态\_电源\_状态\_无效，如果其中一个处于挂起状态。

当以下条件之一为 true 时，泛型父驱动程序挂起设备的 USB 端口：

-   系统正在过渡到较低的电源状态。
-   客户端驱动程序为复合设备上的所有函数已都启动的选择性挂起。

## <a name="related-topics"></a>相关主题
[USB 电源管理](usb-power-management.md)  



