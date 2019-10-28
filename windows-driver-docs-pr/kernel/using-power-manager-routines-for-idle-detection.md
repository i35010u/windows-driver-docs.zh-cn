---
title: 使用电源管理器例程进行空闲检测
description: 使用电源管理器例程进行空闲检测
ms.assetid: 6a89b2eb-d987-4722-b521-9df93153d957
keywords:
- 空闲检测 WDK 电源管理
- PoRegisterDeviceForIdleDetection
- PoSetDeviceBusy
- power manager WDK 内核
- 空闲超时 WDK 电源管理
- 超时 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d11adcb9a98ff1850e07c6ccb407d9f69b93532c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838340"
---
# <a name="using-power-manager-routines-for-idle-detection"></a>使用电源管理器例程进行空闲检测





Power manager 通过[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterdeviceforidledetection)和[**PoSetDeviceBusy**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)例程提供空闲检测支持。

若要为其设备启用空闲检测，设备电源策略所有者将调用**PoRegisterDeviceForIdleDetection**并指定：

-   系统优化性能时要应用的空闲超时值。

-   当系统为节省而优化时要应用的空闲超时值。

-   设备处于空闲状态时应转换为的设备电源状态。

**PoRegisterDeviceForIdleDetection**返回指向空闲计数器的指针，驱动程序稍后使用该计数器禁用空闲检测。 **PoRegisterDeviceForIdleDetection**的调用方必须以 IRQL 运行 &lt; 调度\_级别。

在设备启动并准备好处理设备电源 Irp 之后，驱动程序可以随时注册其设备以进行空闲检测。 例如，驱动程序可能会启用空闲检测作为 PnP 开始设备 IRP 的*IoCompletion*例程的一部分。

任何给定设备的超时值都应与设备的开机延迟以及基于观察到的设备行为成正比。 对于某些类型的设备，驱动程序可以指定 "节省" 和 "性能" 超时值 "-1"，以使用设备类的标准电源策略超时值。 有关详细信息，请参阅设备特定的文档。

设备使用时，驱动程序必须调用[**PoSetDeviceBusy**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)，并传递**PoRegisterDeviceForIdleDetection**返回的指针。 **PoSetDeviceBusy**重置空闲计数器，从而重新启动设备的空闲倒计时。 驱动程序应在每次 i/o 操作时调用**PoSetDeviceBusy** 。

为了确定设备是否处于空闲状态，电源管理器会将空闲计数器的值与当前系统电源策略的驱动程序指定的空闲超时值（保留或性能）进行比较。 有关与系统电源策略相关的功能，请参阅 Microsoft Windows SDK。

当设备满足超时值时，电源管理器会发送设备集电源 IRP，并指定驱动程序在其对**PoRegisterDeviceForIdleDetection**的调用中传递的设备电源状态。 在发送机顶 IRP 之前，电源管理器不会发送查询 IRP。 堆栈中的驱动程序会处理设置电源 IRP，因为这些驱动程序将处理任何其他它们必须及时完成，并且不能对其进行故障转移。 （请参阅[处理设备电源关闭 irp](handling-device-power-down-irps.md)。）

当驱动程序不再需要空闲检测或未准备好处理设备电源关闭 Irp 时，它应再次调用**PoRegisterDeviceForIdleDetection** ，同时为超时值传递零。 如果将超时设置为零，则将禁用节省（电池）和性能（AC）电源策略的空闲检测。 驱动程序可以快速重新启用空闲检测;它只是调用具有非零超时值的**PoRegisterDeviceForIdleDetection** 。 一旦驱动程序注册了设备，它就可以通过更改超时值来启用和禁用空闲检测，即使设备已关闭电源和 reawakened。

 

 




