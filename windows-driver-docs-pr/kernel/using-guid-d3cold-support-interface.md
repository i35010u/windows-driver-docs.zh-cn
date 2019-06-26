---
title: 使用 GUID_D3COLD_SUPPORT_INTERFACE 驱动程序接口
description: 从 Windows 8 开始，驱动程序可以调用例程，以确定设备的 D3cold 功能并启用这些设备使用 D3cold GUID_D3COLD_SUPPORT_INTERFACE 界面中。
ms.assetid: 525637E8-B16F-4038-A78D-A47064E36449
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a83f6b21e1159c198314a88beacb94b360ee378f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381653"
---
# <a name="using-the-guidd3coldsupportinterface-driver-interface"></a>使用 GUID\_D3COLD\_支持\_接口驱动程序接口


从 Windows 8 开始，驱动程序可以调用例程中的 GUID\_D3COLD\_支持\_接口接口来确定设备的 D3cold 功能并启用这些设备使用 D3cold。 此接口中的两个主例程都[ *SetD3ColdSupport* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-set_d3cold_support)并[ *GetIdleWakeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-get_idle_wake_info)。


GUID_D3COLD_SUPPORT_INTERFACE 驱动程序接口提供对 D3 设备电源状态的 D3cold 子状态的支持。 D3 分为两个子状态的状态，D3hot 和 D3cold。 D3 是最低功率设备电源状态，并 D3cold 使用比 D3hot 较少的电量。 设备可以输入 D3cold，仅当设备、 父总线驱动程序和平台固件支持此状态。 支持 D3cold 的设备可以进入和退出此状态时在计算机处于 S0 （工作） 系统电源状态。

设备的电源策略所有者 (PPO) 的驱动程序调用例程在此接口可执行以下操作：

-    发现设备、 父总线驱动程序和平台固件是否支持过渡到 D3cold 子状态。 
-    发现设备的 D3cold 子状态时，设备是否可以发出将唤醒事件发送到处理器。 
-    启用和禁用设备将转换为的 D3cold 子状态。 

若要查询为此接口，设备驱动程序将发送 IRP_MN_QUERY_INTERFACE IRP 关闭驱动程序堆栈。 为此 IRP，驱动程序设置为 GUID_D3COLD_SUPPORT_INTERFACE InterfaceType 输入的参数。 成功完成后的 IRP，接口输出参数是指向 D3COLD_SUPPORT_INTERFACE 结构的指针。 此结构包含在界面中的例程的指针。

有关 D3cold 设备电源状态的详细信息，请参阅[驱动程序中支持 D3cold](supporting-d3cold-in-a-driver.md)。


驱动程序调用*SetD3ColdSupport*例程动态启用和禁用的设备转换为 D3cold 时在计算机处于 S0 可能发生的。 如果设备必须能够从任何低功耗 Dx 状态，则设备将进入信号发生唤醒事件，则驱动程序应启用设备输入 D3cold，仅当设备，可以从 D3cold 发出唤醒事件。 否则，则设备将进入 D3cold 后，可能会不可用计算机离开 S0 状态之前。

默认情况下，首次调用前*SetD3ColdSupport*例程，D3hot D3cold 转换已禁用。 若要更改此默认设置，以便在第一个之前启用 D3hot D3cold 转换*SetD3ColdSupport*调用，该驱动程序包的设备可以包括以下两行 DDInstall.HW 节的 INF 文件安装驱动程序：

```Text
Include = machine.inf
Needs = PciD3ColdSupported
```

*GetIdleWakeInfo*例程，驱动程序，使设备能够发现设备的电源状态从该设备可以发出信号发生唤醒事件时在计算机处于某个特定的系统电源状态。 调用方流入此例程作为输入参数，指定系统电源状态，并作为输出参数，该例程报告最低功率设备电源状态从该设备可以发出信号的等待事件时在计算机处于指定的系统电源状态. 例如， *GetIdleWakeInfo*例程可以告知驱动程序是否在设备可以发出信号发生唤醒事件从 D3cold 时在计算机处于 S0。

*GetIdleWakeInfo*例程提供可从更完整的设备唤醒信息[ **IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求。 此请求，所有版本的 Windows 都支持，提供[**设备\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)结构描述设备的功能。 **DeviceWake**此结构的成员包含的是从可用的信息子集*GetIdleWakeInfo*例程。 此成员指示从其设备可以发出信号等待事件的最低功率设备电源状态。 此成员中的信息保证仅当计算机处于系统低功耗状态所指示的准确**SystemWake**结构中的成员。 如果**SystemWake** = **PowerSystemSleeping3**中的信息**DeviceWake**已知有效适用于 S1 和 S2，S3，经常可能会为其有效和甚至可能适于 S0。

但是，最佳做法是，驱动程序不应假定的中的信息**DeviceWake**方法是对所指示的状态以外的其他任何系统电源状态有效**SystemWake**。 对于某些设备，设备可以从其指示发生唤醒事件的最低 Dx 状态会根据计算机是否处于工作状态 S0 或处于低功耗状态 （S1、 S2、 S3 或 S4） 而有所不同。 对于其他设备，设备连接到总线可以在实际应用时在计算机处于 S0，但设备不能处理唤醒信号。 仅*GetIdleWakeInfo*例程可以准确地描述这些设备的设备唤醒功能。

例如， [PCI Express Base 3.0 规范](https://pcisig.com/specifications/pciexpress/specifications/)定义两个单独的机制，以指示唤醒事件 — PCI Express 链接 （总线） 处于打开状态，且链接处于关闭状态时使用的其他时，使用一种机制。 打开该链接时，设备会发送一串 PM\_PME 事务层数据包 (TLPs) 发出信号，设备应将从低功耗 Dx 状态变为 D0。 链接处于关闭状态，当设备请求是否链接会打开，使设备能够发送 PM\_PME TLPs。 若要请求该链接会打开，该设备，或者断言其唤醒\#信号 （适用于更常见的设备外观造型） 或使用"引导"机制 （不太常见）。

PCI Express 规范要求从 D3cold 播发到信号电源管理事件 (PMEs) 的功能的所有设备都实现这两种设备唤醒机制，但驱动程序开发人员可能需要启用未正确执行的设备实现这些机制。

如果设备可以正确地提供 PM\_PME TLPs 打开该链接时，该驱动程序，即可使设备时在计算机处于 S0 进入 D3hot。 如果设备可以正确断言其唤醒\#发出信号，以打开该链接，然后使用 PM\_PME TLPs 启动转换到 D0，驱动程序，即可使设备时在计算机处于 S0 进入 D3cold。

但是，该驱动程序不应启用设备输入 D3hot 或 D3cold 如果系统固件 (BIOS) 不能保证的硬件平台正确处理 PCI Express 设备唤醒机制。 驱动程序可以调用[ *GetIdleWakeInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-get_idle_wake_info)例程，以发现固件是否声明对这些机制的支持。 如果驱动程序使用内核模式驱动程序框架 (KMDF) 1.11 或更高版本，于调用一个便捷替代方式*GetIdleWakeInfo*是允许[ **WdfDeviceAssignS0IdleSettings** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)方法，以使到空闲中最低驱动 Dx 设备状态从该设备可以发出信号发生唤醒事件。

 

 




