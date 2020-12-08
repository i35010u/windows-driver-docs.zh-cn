---
title: 意外唤醒
description: 意外唤醒是到 D0 的意外转换。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b2eaa94f06179e4b90cbac3c2e2b6146d17b324d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792717"
---
# <a name="surprise-wake-up"></a>意外唤醒


意外唤醒是到 D0 的意外转换。 设备进入 D3cold 后，如果同一电源轨上另一台设备的驱动程序请求从 D3cold 到 D0 的转换，则可能会出现意外唤醒。 第一台设备的驱动程序必须收到意外唤醒的通知，以防止设备处于未初始化的 D0 状态。

当设备从 D3hot 移动到 D3cold 时，可能会出现这种情况，因为它与其他一些设备共享的电源已关闭。 这些设备后的一段时间进入 D3cold，其中一个设备的驱动程序可能会请求转换为 D0。 为响应此请求，父总线驱动程序或 ACPI 筛选器驱动程序将打开电源，并且共享电源的所有设备都将进入其默认的开机硬件状态。

唯一需要此电源状态更改的设备驱动程序是请求更改的驱动程序。 其他设备的驱动程序必须收到此更改的通知，以便他们能够正确地初始化其设备以执行 D0 操作。 只有可接收此通知的驱动程序才能使其设备进入 D3cold。 否则，驱动程序将不知道设备何时进入 D0。

当设备处于开启状态时，它将进入默认的未初始化的硬件状态。 例如， [PCI Express Base 3.0 规范](https://pcisig.com/specifications/pciexpress/specifications/) 定义设备首次接收电源时输入的 *D0 未初始化* 状态。 此状态的定义特定于 PCI Express 设备，而连接到其他总线的设备则用于在打开时输入类似的硬件状态。

对于实现了多个功能的 PCI 或 PCI Express 设备，这些设备功能可能共享相同的电源线。 但是，每个函数可能有一个单独的驱动程序，并且这些函数的驱动程序不太可能直接相互通信。 当其中某个函数的驱动程序请求从 D3cold 到 D0 的电源状态更改时，其他函数的驱动程序将不会进行此更改。 当这些其他函数接收到电源时，必须通知它们的驱动程序，以便可以将这些函数配置为在 D0 中正确运行。

总线驱动程序检测到子设备处于开启状态的时间。 如果此设备的函数驱动程序未请求转换为 D0，则总线驱动程序会提示设备驱动程序向自身发送 D0 电源 IRP ([**irp \_ MN \_ SET \_ power**](./irp-mn-set-power.md) Request with target state = **PowerDeviceD0**) ，以将设备初始化为 D0 操作。 通过此初始化的 D0 状态，设备驱动程序可以启动设备到 D3hot 的转换。 设备驱动程序可以通过以下方式从总线驱动程序接收到 D0 的意外转换通知：

-   直接或间接注册为 [运行时电源管理框架](overview-of-the-power-management-framework.md) 客户端 (PoFx) 接收通知回调的设备驱动程序。
-   Arm 设备用于唤醒的设备的驱动程序将其挂起的 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) 请求由总线驱动程序完成。

从 Windows 8 开始，设备的函数驱动程序作为电源策略所有者，可以将自身注册为 PoFx 的客户端。 当总线驱动程序通知 PoFx 设备遇到了到 D0 的意外转换时，PoFx 可帮助设备转到已初始化的 D0 状态，然后转到 D3hot。 首先，PoFx 调用驱动程序的 [*DevicePowerRequiredCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_required_callback) 例程，以提示设备驱动程序将 D0 电源 IRP 向下发送到设备堆栈。 接下来，PoFx 调用驱动程序的 [*DevicePowerNotRequiredCallback*](/windows-hardware/drivers/ddi/wdm/nc-wdm-po_fx_device_power_not_required_callback) 例程来通知设备驱动程序，设备不需要保持 D0 状态。

从 Kernel-Mode Driver Framework (KMDF) 版本1.11 开始，单组件设备的 KMDF 驱动程序可以通过调用 [**WdfDeviceWdmAssignPowerFrameworkSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicewdmassignpowerframeworksettings) 方法，将其自身直接注册到 PoFx。 在此调用中，驱动程序提供指向回调例程的指针，这些回调例程通知驱动程序到 D0 的意外转换。 有关详细信息，请参阅 [支持功能电源状态](../wdf/supporting-functional-power-states.md)。

如果设备配备为唤醒，则不会向 PoFx 注册其设备的驱动程序仍然会收到意外过渡到 D0 的通知。 当总线驱动程序开启设备电源时，它们会完成驱动程序的 **IRP \_ MN \_ WAIT \_ 唤醒** 请求。 作为响应，驱动程序会将其设备初始化为 D0 操作。 设备可能处于空闲状态，在这种情况下，驱动程序将在一段时间后将此设备移动到 D3hot。

不注册 PoFx 并且不会将其设备用于唤醒的函数驱动程序将不会从 D3cold 到 D0 的意外转换的通知。 设备在未初始化的 D0 状态中可能会花费大量时间。 在此状态下，设备中的所有组件通常都是打开的。 为了降低空闲设备的能耗，驱动程序只应在可以接收到 D0 的意外转换通知时才允许进入 D3cold。

 

