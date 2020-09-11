---
description: 本部分中的主题将探讨 WDM 电源模式与 USB 设备的电源管理属性进行交互的方式。
title: 在 USB 客户端驱动程序中实施电源管理的概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 622e5425650be747cdf1adc6c9bed173f9be062f
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010011"
---
# <a name="overview-of-implementing-power-management-in-usb-client-drivers"></a>在 USB 客户端驱动程序中实施电源管理的概述


本部分中的主题将探讨 WDM 电源模式与 USB 设备的电源管理属性进行交互的方式。

符合通用串行总线 (USB) 规范的 USB 设备的电源管理功能具有丰富且复杂的电源管理功能集。 务必了解这些功能与 Windows 驱动模型 (WDM) 的交互方式，特别是 Microsoft Windows 如何改编标准 USB 功能以支持系统唤醒体系结构。

有关内核模式驱动程序中 WDM 电源管理的信息，请参阅 [实施电源管理](../kernel/introduction-to-power-management.md)。

基于内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 的 USB 客户端驱动程序应使用基本技术和各自框架支持的机制来管理 USB 设备的电源。 有关在基于 KMDF 的客户端驱动程序中管理电源的信息，请参阅 [在驱动程序中支持 PnP 和电源管理](../wdf/supporting-pnp-and-power-management-in-your-driver.md);对于基于 UMDF 的客户端驱动程序，请参阅 [基于 umdf 的驱动程序中的 PnP 和电源管理](../wdf/pnp-and-power-management-in-umdf-drivers.md)。

## <a name="in-this-section"></a>在本节中


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
<td><p><a href="comparing-usb-device-states-to-wdm-device-states.md" data-raw-source="[USB Device Power States](comparing-usb-device-states-to-wdm-device-states.md)">USB 设备电源状态</a></p></td>
<td><p>本主题介绍通用串行总线2.0 规范的9.1 节中指定的 USB 设备电源状态所使用的 WDM 设备状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="selective-suspend-in-usb-drivers-wdf.md" data-raw-source="[Selective suspend in USB drivers (WDF)](selective-suspend-in-usb-drivers-wdf.md)">USB 驱动程序 (WDF) 中的选择性挂起</a></p></td>
<td><p>USB 函数驱动程序通过实现 USB 选择性挂起来支持运行时空闲检测。 下面是有关如何在基于 Windows® Driver Foundation (WDF) 的 USB 驱动程序中实现选择性挂起的驱动程序开发人员的内容。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-selective-suspend.md" data-raw-source="[USB Selective Suspend](usb-selective-suspend.md)">USB 选择性挂起</a></p></td>
<td><p>本部分提供有关为选择性挂起功能选择正确机制的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="register-a-composite-driver.md" data-raw-source="[How to Register a Composite Driver](register-a-composite-driver.md)">如何注册复合驱动程序</a></p></td>
<td><p>本主题介绍了称为复合驱动程序的 USB 多功能设备的驱动程序如何使用基础 USB 驱动程序堆栈注册和注销复合设备。 Microsoft 提供的驱动程序 Usbccgp.sys 是 Windows 加载的默认复合驱动程序。 本主题中的过程适用于自定义 Windows 驱动模型基于 (WDM) 的复合驱动程序，该驱动程序将替换 Usbccgp.sys。</p></td>
</tr>
<tr class="odd">
<td><p><a href="how-to--implement-remote-and-function-wake-support.md" data-raw-source="[How to Implement Function Suspend for a Composite Driver](how-to--implement-remote-and-function-wake-support.md)">如何针对复合驱动程序实施功能挂起</a></p></td>
<td><p>本主题概述了适用于通用串行总线的函数挂起和函数远程唤醒功能 (USB) 3.0 多功能设备 (复合设备) 。 在本主题中，你将了解如何在控制复合设备的驱动程序中实现这些功能。 本主题适用于替换 Usbccgp.sys 的复合驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="remote-wakeup-of-usb-devices.md" data-raw-source="[Remote Wakeup of USB Devices](remote-wakeup-of-usb-devices.md)">远程唤醒 USB 设备</a></p></td>
<td><p>本主题介绍有关在客户端驱动程序中实施远程唤醒功能的最佳实践。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[USB 驱动程序开发指南](usb-driver-development-guide.md)