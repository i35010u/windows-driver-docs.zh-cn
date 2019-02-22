---
title: GPIO 中断
description: 某些常规用途的 I/O (GPIO) 控制器设备可以配置其 GPIO 插针，以充当中断请求输入。
ms.assetid: 0F56AD4C-E0BF-49F1-AB67-0107D08DEF9F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5caf6df9af8a5e6991ccf9154b79f27cffb407be
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532958"
---
# <a name="gpio-interrupts"></a>GPIO 中断


某些常规用途的 I/O (GPIO) 控制器设备可以配置其 GPIO 插针，以充当中断请求输入。 这些中断请求输入是根据物理连接到的 GPIO 插针的外围设备。 这些 GPIO 控制器的驱动程序可以启用、 禁用、 屏蔽、 取消屏蔽，以及清除单个 GPIO 插针上的中断请求。

GPIO 中断的支持是可选的。 GPIO 框架扩展 (GpioClx) 不需要 GPIO 控制器，以支持 GPIO 中断。

## <a name="in-this-section"></a>本部分内容


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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698263" data-raw-source="[Primary and Secondary Interrupts](https://msdn.microsoft.com/library/windows/hardware/hh698263)">主要和次要中断</a></p></td>
<td><p>GPIO 中断处理本质上是一个两阶段过程。 调用从常规用途的 I/O (GPIO) 控制器，它将导致 GPIO framework 扩展 (GpioClx) 中断服务例程 (ISR) 运行，中断<em>主中断</em>。 此 ISR 将中断的 GPIO 插针映射到的全球系统中断 (GSI)，并将此 GSI 传递给硬件抽象层 (HAL)。 生成 HAL<em>辅助中断</em>运行之间存在逻辑连接到的 GPIO 插针此 GSI 通过第二个 ISR。 此过程在关系图中所示<a href="https://msdn.microsoft.com/library/windows/hardware/hh439512#gpio-block-diagram" data-raw-source="[GPIO Driver Support Overview](https://msdn.microsoft.com/library/windows/hardware/hh439512#gpio-block-diagram)">GPIO 驱动程序支持概述</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698246" data-raw-source="[GPIO-Based Interrupt Resources](https://msdn.microsoft.com/library/windows/hardware/hh698246)">基于 GPIO 的中断资源</a></p></td>
<td><p>发送到通用 I/O (GPIO) 插针中断获取作为抽象 Windows GPIO 中断的外围设备的驱动程序中断资源。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff544296" data-raw-source="[Kernel-mode driver framework](https://msdn.microsoft.com/library/windows/hardware/ff544296)">内核模式驱动程序框架</a>(KMDF) 驱动程序收到这些资源通过其<a href="https://msdn.microsoft.com/library/windows/hardware/ff540880" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540880)"> <em>EvtDevicePrepareHardware</em> </a>事件回调函数。 </p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698262" data-raw-source="[Passive-Level ISRs](https://msdn.microsoft.com/library/windows/hardware/hh698262)">被动级别 Isr</a></p></td>
<td><p>作为一个选项，从 Windows 8、 内核模式驱动程序框架 (KMDF) 和用户模式驱动程序框架 (UMDF) 驱动程序可以注册其中断服务例程 (Isr) 在被动级别运行。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698260" data-raw-source="[Interrupt-Related Callbacks](https://msdn.microsoft.com/library/windows/hardware/hh698260)">与中断相关回调</a></p></td>
<td><p>作为一个选项，常规用途的 I/O (GPIO) 控制器的驱动程序可以为 GPIO 中断提供支持。 若要支持 GPIO 中断，GPIO 控制器驱动程序实现了一组回调函数来管理这些中断。 该驱动程序在驱动程序提供时它将自身注册为 GPIO 框架扩展 (GpioClx) 的客户端的注册数据包中包含指向这些回调函数的指针。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/jj851070" data-raw-source="[Interrupt Synchronization for GPIO Controller Drivers](https://msdn.microsoft.com/library/windows/hardware/jj851070)">中断 GPIO 控制器驱动程序的同步</a></p></td>
<td><p>GPIO 控制器驱动程序可以调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439482" data-raw-source="[&lt;strong&gt;GPIO_CLX_AcquireInterruptLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439482)"> <strong>GPIO_CLX_AcquireInterruptLock</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/hh439494" data-raw-source="[&lt;strong&gt;GPIO_CLX_ReleaseInterruptLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439494)"> <strong>GPIO_CLX_ReleaseInterruptLock</strong> </a>方法获取和释放由 GPIO 框架扩展 (GpioClx) 在内部实现的中断锁。 驱动程序代码运行在 IRQL = passive_level 调用可调用这些方法要同步到 GpioClx 中断服务例程 (ISR)。 GpioClx 到引脚 GPIO 控制器中的每个插槽将专用的单独的中断锁。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698245" data-raw-source="[Enabling and Disabling Shared GPIO Interrupts](https://msdn.microsoft.com/library/windows/hardware/hh698245)">启用和禁用共享 GPIO 中断</a></p></td>
<td><p>在某些情况下，中断请求两个或多个外围设备中的行可能会连接到同一个物理通用 I/O (GPIO) pin。 共享的中断行的 GPIO pin 通常配置为使用级别触发中断。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698251" data-raw-source="[GPIO Interrupt Masks](https://msdn.microsoft.com/library/windows/hardware/hh698251)">GPIO 中断掩码</a></p></td>
<td><p>因为中断输入可能是屏蔽和解除屏蔽除了启用和禁用配置的通用 I/O (GPIO) 插针。</p></td>
</tr>
</tbody>
</table>

 

 

 




