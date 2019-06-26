---
title: 意外唤醒
description: 惊讶唤醒是到 D0 的意外的转换。
ms.assetid: 07D3EC05-A1C9-40C5-90FC-E25B5A66B064
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4b777b1e0e48245596cece58b07e5359faa9c465
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385108"
---
# <a name="surprise-wake-up"></a>意外唤醒


惊讶唤醒是到 D0 的意外的转换。 设备进入 D3cold 后，它可能会惊讶唤醒遇到产生了负面影响在相同的电源线上的另一台设备的驱动程序从 D3cold 到 D0 请求转换时的情况。 第一台设备的驱动程序必须接收通知的惊讶唤醒，以防止设备在未初始化的 D0 状态中保留。

当设备从 D3hot 移动到 D3cold 时，它可能是因为它与一定数量的其他设备共享的电源已关闭。 一段时间后这些设备输入 D3cold，一个设备的驱动程序可能会请求转换到 D0。 以响应此请求，父总线驱动程序或 ACPI 筛选器驱动程序打开电源，并共享 power 源的所有设备都输入其默认情况下，电源的硬件状态。

需要此电源状态更改的唯一设备驱动程序是已请求更改的驱动程序。 其他设备的驱动程序必须接收此更改的通知，以便它们可以正确地初始化其设备，以便在 D0 操作。 可以接收此通知的驱动程序应启用输入 D3cold 其设备。 否则，该驱动程序不会知道当设备进入 D0。

启用设备后，它将进入默认情况下，未初始化的硬件状态。 例如， [PCI Express Base 3.0 规范](https://pcisig.com/specifications/pciexpress/specifications/)定义*D0 未初始化的*设备进入当它首次接收电源状态。 此状态的定义是特定于 PCI 和 PCI Express 的设备，但连接到其他总线的设备的设计时它们开启，输入类似硬件状态。

对于实现多个函数的 PCI 或 PCI Express 设备，这些设备函数可能共享相同的电源线。 但是，每个函数可能具有单独的驱动程序，这些函数的驱动程序不太可能直接相互通信。 当这些函数之一的驱动程序请求到 D0 D3cold 电源状态更改时，其他函数的驱动程序不希望此更改。 这些其他函数接收电源，其驱动程序必须收到通知，以便他们可以配置要在 D0 中正常运行的函数。

当子设备的电源打开时，检测到总线驱动程序。 如果此设备的功能驱动程序未请求转换到 D0，总线驱动程序会提示发送本身 D0 power IRP 的设备驱动程序 ( [ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)与目标状态的请求 = **PowerDeviceD0**) 来初始化设备在 D0 操作。 在此初始化 D0 状态下，设备驱动程序然后可以启动设备的过渡到 D3hot。 设备驱动程序可以接收通知的意外转换到 D0 总线驱动程序从以下方面：

-   直接或间接地将自己注册为的客户端的设备驱动程序[运行电源管理框架](overview-of-the-power-management-framework.md)(PoFx) 接收通知回调。
-   适用于 arm 唤醒其设备的设备驱动程序都有其挂起[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake)总线驱动程序已完成的请求。

从 Windows 8 开始，设备的功能驱动程序，充当电源策略所有者，可以注册其自身作为 PoFx 的客户端。 当总线驱动程序通知设备遇到意外转换到 D0 PoFx 时，PoFx 可帮助移动到未初始化的 D0 状态，然后向 D3hot 移动设备。 首先，PoFx 调用驱动程序的[ *DevicePowerRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_required_callback)例程，以提示发送关闭设备堆栈 D0 电源 IRP 的设备驱动程序。 接下来，PoFx 调用驱动程序的[ *DevicePowerNotRequiredCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-po_fx_device_power_not_required_callback)例程，以通知不是设备的设备驱动程序所需处于 D0 状态。

开始使用内核模式驱动程序框架 (KMDF) 版本 1.11 KMDF 驱动程序的单一组件设备可以间接自身注册 PoFx 通过调用[ **WdfDeviceWdmAssignPowerFrameworkSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings)方法。 在此调用中，驱动程序提供通知的意外转换到 D0 驱动程序的回调例程的指针。 有关详细信息，请参阅[支持功能的电源状态](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-functional-power-states)。

如果设备有唤醒，则仍可以向 D0 意外转换的通知不会与 PoFx 注册其设备驱动程序。 当总线驱动程序打开到设备的电源时，他们完成的驱动程序**IRP\_MN\_等待\_唤醒**请求。 在响应中，该驱动程序初始化其设备时在 D0 操作。 设备很可能处于空闲状态，在这种情况下该驱动程序，一段时间后将进入此设备 D3hot。

功能驱动程序，不会与 PoFx 注册和，不会不 arm 唤醒其设备收到意外转换的任何通知 D3cold D0。 设备可能会花费大量时间的未初始化的 D0 状态。 在此状态下，所有设备中的组件通常打开的。 若要减少的空闲状态的设备的功率消耗，驱动程序应仅在他们可以接收通知的意外转换到 D0 启用 D3cold 的条目。

 

 




