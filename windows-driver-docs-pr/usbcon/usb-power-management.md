---
Description: 在本部分中的主题检查 WDM 电源模型与 USB 设备的电源管理属性交互的方式。
title: 在 USB 客户端驱动程序中实施电源管理的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bec2d1b76c409434542eb19d1d80c65c3ef8dc0c
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717017"
---
# <a name="overview-of-implementing-power-management-in-usb-client-drivers"></a>在 USB 客户端驱动程序中实施电源管理的概述


在本部分中的主题检查 WDM 电源模型与 USB 设备的电源管理属性交互的方式。

符合通用串行总线 (USB) 规范的 USB 设备的电源管理功能具有丰富和复杂一的电源管理功能。 务必要了解这些功能的交互方式使用 Windows 驱动程序模型 (WDM) 中，并特别是 Microsoft Windows 如何了调整，使标准 USB 功能来支持系统唤醒体系结构。

WDM 内核模式驱动程序中的电源管理有关的信息，请参阅[实施电源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-power-management)。

USB 客户端驱动程序在内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 应使用支持的基本技术和相应框架，可用于管理电源的 USB 设备的机制。 有关管理 KMDF 基于客户端驱动程序中的能力的信息，请参阅[支持即插即用和您的驱动程序中的电源管理](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-pnp-and-power-management-in-your-driver); 对于 UMDF 基于客户端驱动程序，请参阅[基于 UMDF 驱动程序中的PnP和电源管理](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-in-umdf-drivers).

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="comparing-usb-device-states-to-wdm-device-states.md" data-raw-source="[USB Device Power States](comparing-usb-device-states-to-wdm-device-states.md)">USB 设备的电源状态</a></p></td>
<td><p>本主题介绍了要使用 USB 设备电源状态为指定的通用串行总线 2.0 规范的 9.1 节中的 WDM 设备状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="selective-suspend-in-usb-drivers-wdf.md" data-raw-source="[Selective suspend in USB drivers (WDF)](selective-suspend-in-usb-drivers-wdf.md)">USB 驱动程序 (WDF) 中的选择性挂起</a></p></td>
<td><p>USB 函数驱动程序支持运行时空闲检测通过实现 USB 选择性挂起。 下面是有关如何实现选择性的驱动程序开发人员挂起基于 Windows® Driver Foundation (WDF) 上的 USB 驱动程序中的内容。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-selective-suspend.md" data-raw-source="[USB Selective Suspend](usb-selective-suspend.md)">USB 选择性挂起</a></p></td>
<td><p>本部分提供有关选择正确的机制的选择性挂起功能的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="register-a-composite-driver.md" data-raw-source="[How to Register a Composite Driver](register-a-composite-driver.md)">如何注册复合驱动程序</a></p></td>
<td><p>本主题介绍如何称为复合驱动程序，USB 多功能设备的驱动程序可以注册和注销的复合设备与基础的 USB 驱动程序堆栈。 Microsoft 提供驱动程序，Usbccgp.sys，是由 Windows 加载默认复合驱动程序。 本主题中的过程适用于自定义 Windows 驱动程序模型 WDM 基于复合驱动程序，用于替换 Usbccgp.sys。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to--implement-remote-and-function-wake-support.md" data-raw-source="[How to Implement Function Suspend for a Composite Driver](how-to--implement-remote-and-function-wake-support.md)">如何实现复合的驱动程序函数挂起</a></p></td>
<td><p>本主题提供的函数概述挂起和函数远程唤醒功能的通用串行总线 (USB) 3.0 的多功能设备 （复合设备）。 本主题中将学习如何在控制复合设备的驱动程序中实现这些功能。 本主题适用于复合替换 Usbccgp.sys 的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="remote-wakeup-of-usb-devices.md" data-raw-source="[Remote Wakeup of USB Devices](remote-wakeup-of-usb-devices.md)">远程唤醒的 USB 设备</a></p></td>
<td><p>本主题介绍有关在客户端驱动程序中实现远程唤醒功能的最佳做法。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)  



