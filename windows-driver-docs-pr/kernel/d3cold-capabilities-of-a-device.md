---
title: 设备的 D3cold 功能
description: 在设备的电源策略所有者（PPO）的驱动程序允许设备进入 "D3cold" （当计算机停留在 S0 中时）之前，驱动程序必须验证设备是否响应并在设备进入 D3cold 后继续正常运行。
ms.assetid: 5A6CB076-7D97-48EC-B2BF-3204CD093B3E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4d89053138d87abd38e2a6b555c65f4f4c6fb819
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828438"
---
# <a name="d3cold-capabilities-of-a-device"></a>设备的 D3cold 功能


在设备的电源策略所有者（PPO）的驱动程序允许设备进入 "D3cold" （当计算机停留在 S0 中时）之前，驱动程序必须验证设备是否响应并在设备进入 D3cold 后继续正常运行。

对于即插即用（PnP）设备，操作系统通常从父总线驱动程序获取有关设备的 D3cold 功能的信息。

例如，如果将设备连接到 PCI Express 或 PCI Express 总线，则设备的 PCI 配置空间将包含表示设备功能的电源管理注册块。 此块中的功能标志指定设备的电源状态，设备可从该电源状态发出电源管理事件或 PME （唤醒事件的 PCI 术语）。 这些状态可能包括 D3hot 和 D3cold。 有关 PCI 电源管理的详细信息，请参阅[Pci 总线电源管理接口规范](https://pcisig.com/specifications/conventional/pci_bus_power_management_interface/)。

如果设备必须能够从其输入的任何低功耗 Dx 状态向唤醒事件发出信号，则设备不应输入 D3cold，除非设备、父总线控制器和硬件平台支持从 D3cold 发出唤醒事件。

设备的 KMDF 驱动程序将调用[**WdfDeviceAssignS0IdleSettings**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)方法，以使设备能够在设备可用于传输唤醒事件的最小设备电源状态中处于空闲状态。 从 KMDF 版本1.11 开始， **WdfDeviceAssignS0IdleSettings**在可能的低功耗 Dx 状态范围内包含 D3cold。 仅当设备、父总线驱动程序和 ACPI 系统固件支持 D3cold 发出的唤醒事件时，此方法才允许设备在 D3cold 中空闲。

设备的 WDM 驱动程序必须决定设备处于空闲状态时要将设备移动到哪种低功耗 Dx 状态。 （相反， **WdfDeviceAssignS0IdleSettings**会自动选择此 Dx 状态，以便驱动程序不需要。）如果设备必须能够从其输入的任何低功耗 Dx 状态向唤醒事件发出信号，则驱动程序可以调用[*GetIdleWakeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)例程来确定设备可用于向唤醒事件发出信号的最小设备电源状态。 为获取此信息， *GetIdleWakeInfo*会查询底层总线驱动程序和 ACPI 系统固件。 根据*GetIdleWakeInfo*中的信息，驱动程序可以调用[*SetD3ColdSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support)例程来启用或禁用设备到 D3cold 的转换。

设备可能不需要能够从 D3cold 发出唤醒事件。 仅当响应软件启动的操作时，才可以将设备设置为仅允许从 D3cold 到 D0 的转换。 例如，如果驱动程序收到设备的 i/o 请求，驱动程序可能需要唤醒设备。 除了少数例外情况，此类设备的驱动程序可以使设备进入 D3cold。 一个可能的例外是需要很长时间才能将 D3cold 转换为 D0 的设备。 例如，显示设备可能包含大量需要在设备进入 D3cold 之前保存并在设备退出 D3cold 之后进行还原的内存。

有关 D3cold 的 ACPI 支持的详细信息，请参阅[D3cold 的固件要求](https://docs.microsoft.com/windows-hardware/drivers/bringup/firmware-requirements-for-d3cold)。

 

 




