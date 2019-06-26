---
title: 标准驱动程序例程简介
description: 标准驱动程序例程简介
ms.assetid: 91aaca02-a571-4058-b5af-98277fcbcf9d
keywords:
- 标准驱动程序例程 WDK 内核，有关标准驱动程序例程
- 驱动程序例程 WDK 内核，有关标准驱动程序例程
- 例程 WDK 内核，有关标准驱动程序例程
- Irp WDK 内核，标准驱动程序例程
- 所需的标准例程 WDK 内核
- 可选的标准例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1e14a41845861e74c0872cc2dea08290bcf1297
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386590"
---
# <a name="introduction-to-standard-driver-routines"></a>标准驱动程序例程简介





每个内核模式驱动程序会构造一组系统定义的标准驱动程序例程。 内核模式驱动程序进程*I/O 请求数据包*(Irp) 这些标准例程通过调用系统提供的驱动程序支持例程中。

所有驱动程序，而不考虑其级别的附加驱动程序，链中必须具有一组基本的标准例程才能处理 Irp。 驱动程序是否必须实现其他标准例程取决于驱动程序控制物理设备还是通过物理设备驱动程序，以及基础物理设备的性质进行分层。 控制物理设备的最低级别驱动程序具有更需要的例程比更高级别的驱动程序，它通常将 Irp 传递到较低的驱动程序进行处理。

标准驱动程序例程可以分为两个组： 必须拥有每个内核模式驱动程序，以及是可选的具体取决于驱动程序类型和位置*设备堆栈*。

本部分介绍了所需的标准例程。 其他部分描述了可选的例程。

以下是两个表。 第一个表列出了所需的标准例程。 第二个列出可选例程的大多数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>所需的标准驱动程序例程</th>
<th>用途</th>
<th>所描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize">DriverEntry</a></strong></p></td>
<td><p>初始化该驱动程序和其驱动程序对象。</p></td>
<td><p><a href="writing-a-driverentry-routine.md" data-raw-source="[Writing a DriverEntry Routine](writing-a-driverentry-routine.md)">编写 DriverEntry 例程</a></p></td>
</tr>
<tr class="even">
<td><p><em><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device">AddDevice</a></em></p></td>
<td><p>初始化设备并创建设备对象。</p></td>
<td><p><a href="writing-an-adddevice-routine.md" data-raw-source="[Writing an AddDevice Routine](writing-an-adddevice-routine.md)">编写 AddDevice 例程</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/dispatchcreate--dispatchclose--and-dispatchcreateclose-routines">调度例程</a></p></td>
<td><p>接收和处理 Irp。</p></td>
<td><p><a href="writing-dispatch-routines.md" data-raw-source="[Writing Dispatch Routines](writing-dispatch-routines.md)">写入调度例程</a></p></td>
</tr>
<tr class="even">
<td><p><em>卸载</em></p></td>
<td><p>释放系统资源获取驱动程序。</p></td>
<td><p><a href="writing-an-unload-routine.md" data-raw-source="[Writing an Unload Routine](writing-an-unload-routine.md)">编写卸载例程</a></p></td>
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
<th>可选的标准驱动程序例程</th>
<th>用途</th>
<th>所描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>重新初始化</em></p></td>
<td><p>如果完成驱动程序初始化<strong>DriverEntry</strong>不能。</p></td>
<td><p><a href="writing-a-reinitialize-routine.md" data-raw-source="[Writing a Reinitialize Routine](writing-a-reinitialize-routine.md)">写入一个重新初始化例程</a></p></td>
</tr>
<tr class="even">
<td><p><em>StartIo</em></p></td>
<td><p>启动物理设备上的 I/O 操作。</p></td>
<td><p><a href="writing-a-startio-routine.md" data-raw-source="[Writing a StartIo Routine](writing-a-startio-routine.md)">编写 StartIo 例程</a></p></td>
</tr>
<tr class="odd">
<td><p>中断服务例程</p></td>
<td><p>这将中断时，将保存设备状态。</p></td>
<td><p><a href="writing-an-isr.md" data-raw-source="[Writing an ISR](writing-an-isr.md)">编写 ISR</a></p></td>
</tr>
<tr class="even">
<td><p>延迟的过程调用</p></td>
<td><p>完成设备中断处理之后 ISR 保存设备状态。</p></td>
<td><p><a href="dpc-objects-and-dpcs.md" data-raw-source="[DPC Objects and DPCs](dpc-objects-and-dpcs.md)">DPC 对象和 dpc 进行标记</a></p></td>
</tr>
<tr class="odd">
<td><p><em>SynchCritSection</em></p></td>
<td><p>同步对驱动程序数据的访问。</p></td>
<td><p><a href="using-critical-sections.md" data-raw-source="[Using Critical Sections](using-critical-sections.md)">使用关键节</a></p></td>
</tr>
<tr class="even">
<td><p><em>AdapterControl</em></p></td>
<td><p>启动 DMA 操作。</p></td>
<td><p><a href="adapter-objects-and-dma.md" data-raw-source="[Adapter Objects and DMA](adapter-objects-and-dma.md)">适配器对象和 DMA</a></p></td>
</tr>
<tr class="odd">
<td><p><em>IoCompletion</em></p></td>
<td><p>完成的 IRP 的驱动程序的处理。</p></td>
<td><p><a href="completing-irps.md" data-raw-source="[Completing IRPs](completing-irps.md)">完成 Irp</a></p></td>
</tr>
<tr class="even">
<td><p><em>取消</em></p></td>
<td><p>取消的 IRP 的驱动程序的处理。</p></td>
<td><p><a href="canceling-irps.md" data-raw-source="[Canceling IRPs](canceling-irps.md)">正在取消 Irp</a></p></td>
</tr>
<tr class="odd">
<td><p><em>CustomTimerDpc</em>， <em>IoTimer</em></p></td>
<td><p>计时和同步事件。</p></td>
<td><p><a href="synchronization-techniques.md" data-raw-source="[Synchronization Techniques](synchronization-techniques.md)">同步技术</a></p></td>
</tr>
</tbody>
</table>

 

当前的 IRP 和目标设备对象是很多标准例程的输入的参数。 每个驱动程序处理每个 IRP 分阶段通过其组的标准例程。

按照约定，前面添加系统提供的驱动程序，除每个标准例程名称标识的、 特定于驱动程序或设备特定前缀**DriverEntry**。 例如，本文档使用"DD"，如中所示[驱动程序对象图](introduction-to-driver-objects.md#driver-object-illustration)。 遵循此约定可以更轻松地调试和维护的驱动程序。

 

 




