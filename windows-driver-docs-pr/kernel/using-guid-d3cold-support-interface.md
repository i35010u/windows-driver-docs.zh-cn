---
title: 使用 GUID_D3COLD_SUPPORT_INTERFACE 驱动程序接口
description: 从 Windows 8 开始，驱动程序可以调用 GUID_D3COLD_SUPPORT_INTERFACE 接口中的例程来确定设备的 D3cold 功能，并使这些设备能够使用 D3cold。
ms.assetid: 525637E8-B16F-4038-A78D-A47064E36449
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 026f9173c9b66bad4d02df32f2309c874b087847
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184975"
---
# <a name="using-the-guid_d3cold_support_interface-driver-interface"></a>使用 GUID \_ D3COLD \_ 支持 \_ 接口驱动程序接口


从 Windows 8 开始，驱动程序可以调用 GUID \_ D3COLD \_ 支持接口接口中的例程 \_ 来确定设备的 D3COLD 功能，并允许这些设备使用 D3COLD。 此接口中的两个主要例程是 [*SetD3ColdSupport*](/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support) 和 [*GetIdleWakeInfo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info)。


GUID_D3COLD_SUPPORT_INTERFACE 驱动程序接口支持 D3 设备电源状态的 D3cold 子状态。 D3 分为两个 substates： D3hot 和 D3cold。 D3 是功率最低的设备电源状态，D3cold 使用比 D3hot 更少的功率。 仅当设备、父总线驱动程序和平台固件支持此状态时，设备才可以输入 D3cold。 当计算机处于 S0 () 系统电源状态时，支持 D3cold 的设备可以进入和退出此状态。

作为设备的电源策略所有者 (PPO) 的驱动程序将调用此接口中的例程来执行以下操作：

-    查明设备、父总线驱动程序和平台固件是否支持转换为 D3cold 子查询。 
-    发现设备处于 D3cold 子查询时，设备是否可以向处理器发出唤醒事件信号。 
-    启用和禁用设备对 D3cold 子情况的转换。 

若要查询此接口，设备驱动程序将 IRP_MN_QUERY_INTERFACE IRP 向下发送驱动程序堆栈。 对于此 IRP，驱动程序将 InterfaceType 输入参数设置为 GUID_D3COLD_SUPPORT_INTERFACE。 成功完成 IRP 后，接口输出参数是指向 D3COLD_SUPPORT_INTERFACE 结构的指针。 此结构包含指向接口中的例程的指针。

有关 D3cold 设备电源状态的详细信息，请参阅 [在驱动程序中支持 D3cold](supporting-d3cold-in-a-driver.md)。


驱动程序调用 *SetD3ColdSupport* 例程以动态地启用和禁用设备到 D3cold 的转换，该转换可能在计算机处于 S0 时出现。 如果设备必须能够从设备输入的任何低功耗 Dx 状态向唤醒事件发出信号，则驱动程序应使设备仅在设备可从 D3cold 发出唤醒事件信号时才输入 D3cold。 否则，在设备进入 D3cold 后，它可能不可用，直到计算机离开 S0 状态。

默认情况下，在首次调用 *SetD3ColdSupport* 例程之前，将禁用 D3hot 到 D3cold 转换。 若要更改此默认设置，以便在第一个 *SetD3ColdSupport* 调用之前启用 D3hot 到 D3cold 的转换，设备的驱动程序包可以在安装驱动程序的 INF 文件的 DDInstall 部分中包含以下两行：

```Text
Include = machine.inf
Needs = PciD3ColdSupported
```

*GetIdleWakeInfo*例程允许设备的驱动程序发现设备电源状态，在计算机处于特定系统电源状态时，设备可以通过此状态向唤醒事件发出信号。 此例程的调用方将系统电源状态指定为输入参数，并将其作为输出参数，它会报告在计算机处于指定系统电源状态时，设备可向等待事件发出信号的最小设备电源状态。 例如，当计算机处于 S0 时， *GetIdleWakeInfo* 例程可以告知驱动程序设备是否可以从 D3cold 发出唤醒事件信号。

*GetIdleWakeInfo*例程提供的设备唤醒信息比[**IRP \_ MN \_ 查询 \_ 功能**](./irp-mn-query-capabilities.md)请求提供的更完整。 此请求（所有版本的 Windows 支持）提供了描述设备功能的 [**设备 \_ 功能**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities) 结构。 此结构的 **DeviceWake** 成员包含 *GetIdleWakeInfo* 例程中提供的信息的子集。 此成员指示设备可用于向等待事件发出信号的最小设备电源状态。 仅当计算机处于该结构的 **SystemWake** 成员所指示的系统低功耗状态时，才保证此成员中的信息是准确的。 如果**SystemWake**  =  **PowerSystemSleeping3**，则**DeviceWake**中的信息已知对 S3 有效，可能常常对 S1 和 S2 有效，甚至对 S0 有效。

但是，作为最佳做法，驱动程序不应假定 **DeviceWake** 方法中的信息对于除 **SystemWake**指示的状态之外的任何系统电源状态有效。 对于某些设备，设备可向其发出唤醒事件信号的最小 Dx 状态因计算机处于工作状态 S0 还是低功耗状态 (S1、S2、S3 或 S4) 而异。 对于其他设备，设备连接到的总线可以在计算机处于 S0 中时处理唤醒信号，但设备不能。 只有 *GetIdleWakeInfo* 例程才能准确描述这些设备的设备唤醒功能。

例如， [Pci Express Base 3.0 规范](https://pcisig.com/specifications/pciexpress/specifications/) 定义了两个单独的机制来对唤醒事件发出信号，其中一种机制是在 PCI express 链接 (的总线) 打开时使用，另一种机制在关闭链接时使用。 当打开该链接时，设备将发送一个 PM \_ PME 事务层包流 (TLPs) ，以指示设备应从低功耗 Dx 状态移动到 D0。 关闭该链接后，设备会请求打开该链接，使设备能够发送 PM \_ PME TLPs。 若要请求打开链接，设备会将其唤醒 \# 信号断言 (更常见的设备外形规格) 或使用 "引导" 机制 (不太常见的) 。

PCI Express 规范要求所有提供通知电源管理事件功能的设备 (PMEs) 从 D3cold 实现这两种设备唤醒机制，但驱动程序开发人员可能需要启用无法正确实现这些机制的设备。

如果在打开链接时，设备可以正确交付 PM \_ PME TLPs，则驱动程序可以使设备在计算机处于 S0 时进入 D3hot。 如果设备可以正确地断言其唤醒 \# 信号来打开链接，然后使用 PM \_ PME TLPs 启动到 D0 的转换，则驱动程序可以使设备在计算机处于 S0 中时进入 D3cold。

但是，如果系统固件 (BIOS) 无法保证 PCI Express 设备唤醒机制已由硬件平台正确处理，则驱动程序不能让设备输入 D3hot 或 D3cold。 驱动程序可以调用 [*GetIdleWakeInfo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info) 例程来发现固件是否支持这些机制。 如果驱动程序使用内核模式驱动程序框架 (KMDF) 1.11 或更高版本，则调用 *GetIdleWakeInfo* 的一种方便的替代方法是允许 [**WdfDeviceAssignS0IdleSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings) 方法让设备在设备可通过其发出唤醒事件信号的最的 Dx 状态下空闲。

 

