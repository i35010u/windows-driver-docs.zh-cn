---
title: 标准驱动程序例程简介
description: 标准驱动程序例程简介
keywords:
- 标准驱动程序例程 WDK 内核，关于标准驱动程序例程
- 驱动程序例程 WDK 内核，关于标准驱动程序例程
- 例程的 WDK 内核，关于标准驱动程序例程
- Irp WDK 内核，标准驱动程序例程
- 必需的标准例程 WDK 内核
- 可选标准例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e6fb1f9d2872d7efa5d30b0d4e0c40e13962b69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838877"
---
# <a name="introduction-to-standard-driver-routines"></a>标准驱动程序例程简介





每个内核模式驱动程序都围绕一组系统定义的标准驱动程序例程构造。 内核模式驱动程序通过调用系统提供的驱动程序支持例程来处理 (Irp) 在这些标准例程内的 *i/o 请求包* 。

无论驱动程序在附加驱动程序链中的级别如何，所有驱动程序都必须具有一组基本的标准例程才能处理 Irp。 驱动程序是否必须实现额外的标准例程取决于驱动程序是控制物理设备还是控制物理设备驱动程序，以及基础物理设备的性质。 控制物理设备的最低级别驱动程序所需的例程比高级驱动程序要多，后者通常将 Irp 传递到较低的驱动程序以进行处理。

标准驱动程序例程可以分为两组：每个内核模式驱动程序必须具有的组和可选的组，具体取决于 *设备堆栈* 中的驱动程序类型和位置。

本部分介绍所需的标准例程。 其他部分描述了可选例程。

下面是两个表。 第一个表列出了所需的标准例程。 第二个表列出了大多数可选例程。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>必需的标准驱动程序例程</th>
<th>目的</th>
<th>描述位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize">DriverEntry</a></strong></p></td>
<td><p>初始化驱动程序及其驱动程序对象。</p></td>
<td><p><a href="writing-a-driverentry-routine.md" data-raw-source="[Writing a DriverEntry Routine](writing-a-driverentry-routine.md)">编写 DriverEntry 例程</a></p></td>
</tr>
<tr class="even">
<td><p><em><a href="/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device">AddDevice</a></em></p></td>
<td><p>初始化设备并创建设备对象。</p></td>
<td><p><a href="writing-an-adddevice-routine.md" data-raw-source="[Writing an AddDevice Routine](writing-an-adddevice-routine.md)">编写 AddDevice 例程</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/kernel/dispatchcreate--dispatchclose--and-dispatchcreateclose-routines">Dispatch 例程</a></p></td>
<td><p>接收和处理 Irp。</p></td>
<td><p><a href="writing-dispatch-routines.md" data-raw-source="[Writing Dispatch Routines](writing-dispatch-routines.md)">编写 Dispatch 例程</a></p></td>
</tr>
<tr class="even">
<td><p><em>[</em></p></td>
<td><p>释放驱动程序获取的系统资源。</p></td>
<td><p><a href="writing-an-unload-routine.md" data-raw-source="[Writing an Unload Routine](writing-an-unload-routine.md)">编写 Unload 例程</a></p></td>
</tr>
</tbody>
</table>

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>可选标准驱动程序例程</th>
<th>目的</th>
<th>描述位置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>初始化</em></p></td>
<td><p>如果 <strong>DriverEntry</strong> 无法完成驱动程序初始化。</p></td>
<td><p><a href="writing-a-reinitialize-routine.md" data-raw-source="[Writing a Reinitialize Routine](writing-a-reinitialize-routine.md)">编写 Reinitialize 例程</a></p></td>
</tr>
<tr class="even">
<td><p><em>StartIo</em></p></td>
<td><p>在物理设备上启动 i/o 操作。</p></td>
<td><p><a href="writing-a-startio-routine.md" data-raw-source="[Writing a StartIo Routine](writing-a-startio-routine.md)">编写 StartIo 例程</a></p></td>
</tr>
<tr class="odd">
<td><p>中断服务例程</p></td>
<td><p>在设备中断时保存设备的状态。</p></td>
<td><p><a href="writing-an-isr.md" data-raw-source="[Writing an ISR](writing-an-isr.md)">编写 ISR</a></p></td>
</tr>
<tr class="even">
<td><p>延迟的过程调用</p></td>
<td><p>在 ISR 保存设备状态之后完成设备中断的处理。</p></td>
<td><p><a href="/windows-hardware/drivers/kernel/introduction-to-dpc-objects">DPC 对象和 DPC</a></p></td>
</tr>
<tr class="odd">
<td><p><em>SynchCritSection</em></p></td>
<td><p>同步对驱动程序数据的访问。</p></td>
<td><p><a href="using-critical-sections.md" data-raw-source="[Using Critical Sections](using-critical-sections.md)">使用关键节</a></p></td>
</tr>
<tr class="even">
<td><p><em>AdapterControl</em></p></td>
<td><p>启动 DMA 操作。</p></td>
<td><p><a href="/windows-hardware/drivers/kernel/introduction-to-adapter-objects" data-raw-source="[Adapter Objects and DMA](./introduction-to-adapter-objects.md)">适配器对象和 DMA</a></p></td>
</tr>
<tr class="odd">
<td><p><em>IoCompletion</em></p></td>
<td><p>完成对 IRP 的处理。</p></td>
<td><p><a href="completing-irps.md" data-raw-source="[Completing IRPs](completing-irps.md)">完成 IRP</a></p></td>
</tr>
<tr class="even">
<td><p><em>取消</em></p></td>
<td><p>取消驱动程序的 IRP 处理。</p></td>
<td><p><a href="canceling-irps.md" data-raw-source="[Canceling IRPs](canceling-irps.md)">取消 IRP</a></p></td>
</tr>
<tr class="odd">
<td><p><em>CustomTimerDpc</em>、 <em>IoTimer</em></p></td>
<td><p>计时和同步事件。</p></td>
<td><p><a href="/windows-hardware/drivers/kernel/introduction-to-kernel-dispatcher-objects">同步技术</a></p></td>
</tr>
</tbody>
</table>

 

当前 IRP 和目标设备对象是许多标准例程的输入参数。 每个驱动程序都通过其一组标准例程处理每个 IRP。

按照约定，系统提供的驱动程序会在除 **DriverEntry** 之外的每个标准例程的名称前面预置标识、驱动程序特定的或特定于设备的前缀。 例如，本文档使用 "DD"，如 [驱动程序对象简介](introduction-to-driver-objects.md)中所示。 遵循此约定可以更轻松地调试和维护驱动程序。

