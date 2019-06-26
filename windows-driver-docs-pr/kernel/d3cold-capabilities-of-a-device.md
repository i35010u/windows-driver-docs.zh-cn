---
title: 设备的 D3cold 功能
description: 是设备的电源策略所有者 (PPO) 的驱动程序会启用设备输入 D3cold （当该计算机是保留在 S0） 之前，设备将立即响应并继续正常运行，则设备将进入 D3cold 后必须验证该驱动程序。
ms.assetid: 5A6CB076-7D97-48EC-B2BF-3204CD093B3E
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7ffca85cfc5c68ab6dd994e4ddb15dd4ba8f1235
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377135"
---
# <a name="d3cold-capabilities-of-a-device"></a>设备的 D3cold 功能


是设备的电源策略所有者 (PPO) 的驱动程序会启用设备输入 D3cold （当该计算机是保留在 S0） 之前，设备将立即响应并继续正常运行，则设备将进入 D3cold 后必须验证该驱动程序。

Plug and Play (PnP) 设备的操作系统通常从父总线驱动程序获取 D3cold 功能的设备信息。

例如，如果设备已附加到 PCI 或 PCI Express 总线，设备的 PCI 配置空间包含 Power 管理注册块，用于指示设备的功能。 此块中的功能标志指定设备的电源状态从该设备可以发出信号电源管理事件或 PME （唤醒事件 PCI 词）。 这些状态可能包括 D3hot 和 D3cold。 有关 PCI 电源管理的详细信息，请参阅[PCI 总线电源管理接口规范](https://pcisig.com/specifications/conventional/pci_bus_power_management_interface/)。

如果设备必须能够从进入任何低功耗 Dx 状态信号发生唤醒事件，则设备不应进入 D3cold 除非设备、 父总线控制器和硬件平台支持从 D3cold 信号发生唤醒事件。

设备 KMDF 驱动程序调用[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)方法，以使到空闲的最低功率设备电源状态从该设备可以发出信号发生唤醒事件中的设备。 从开始 KMDF 版本 1.11 **WdfDeviceAssignS0IdleSettings**包括 D3cold 范围内的可能的低功率 Dx 状态。 此方法启用设备、 父总线驱动程序和 ACPI 系统固件支持 D3cold 信号唤醒事件时，才在 D3cold 空闲的设备。

设备 WDM 驱动程序必须确定要将设备移到该设备处于空闲状态时的低功耗 Dx 状态。 (与此相反， **WdfDeviceAssignS0IdleSettings** ，以便该驱动程序不会自动选择此 Dx 状态。)如果设备必须能够从进入任何低功耗 Dx 状态信号发生唤醒事件，该驱动程序可以调用[ *GetIdleWakeInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-get_idle_wake_info)例程，以确定从中的最低功率设备电源状态设备可以发出信号发生唤醒事件。 若要获得此信息，请*GetIdleWakeInfo*查询基础总线驱动程序和 ACPI 系统固件。 根据从信息*GetIdleWakeInfo*，该驱动程序可以调用[ *SetD3ColdSupport* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-set_d3cold_support)例程，以启用或禁用设备的转换为 D3cold。

设备可能不需要从 D3cold 信号发生唤醒事件的能力。 设备是可能所需以进行从 D3cold 到转换 D0 仅在响应软件启动的操作。 例如，驱动程序可能需要以唤醒设备，如果该驱动程序收到设备的 I/O 请求。 几个例外情况之外，此类设备的驱动程序可以使设备能够输入 D3cold。 一个可能的例外是需要大量时间对 D0 从 D3cold 进行转换的设备。 例如，显示设备可能包含大量的内存，需要先在设备进入 D3cold 保存并还原设备退出 D3cold 后。

有关对 D3cold ACPI 支持的详细信息，请参阅[D3cold 固件要求](https://docs.microsoft.com/windows-hardware/drivers/bringup/firmware-requirements-for-d3cold)。

 

 




