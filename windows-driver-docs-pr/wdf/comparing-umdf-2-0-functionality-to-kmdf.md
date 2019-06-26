---
title: 比较 UMDF 2 的 KMDF 的功能
description: 本主题将比较可用于的内核模式驱动程序框架 (KMDF) 驱动程序和功能，可用于用户模式驱动程序框架 (UMDF) 2 驱动程序。
ms.assetid: 9D4DD1A9-DA49-4132-B98F-AFEC8B427272
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8790f4013e8521677ac410c2e658213c11a1d635
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382886"
---
# <a name="comparing-umdf-2-functionality-to-kmdf"></a>比较 UMDF 2 的 KMDF 的功能


本主题将比较可用于的内核模式驱动程序框架 (KMDF) 驱动程序和功能，可用于用户模式驱动程序框架 (UMDF) 2 驱动程序。 它旨在帮助您决定是否应写入 UMDF 2 驱动程序或 KMDF 驱动程序。

虽然 UMDF 版本 2 提供了以前只能用于 KMDF 驱动程序功能的重要部分，可以仅适用于 KMDF 驱动程序的以下功能。 如果您的驱动程序需要这些功能之一，则必须编写 KMDF 驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">功能</th>
<th align="left">相关的信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">直接内存访问 (DMA)</td>
<td align="left"><a href="handling-dma-operations-in-kmdf-drivers.md" data-raw-source="[Handling DMA Operations in KMDF Drivers](handling-dma-operations-in-kmdf-drivers.md)">处理 DMA KMDF 驱动程序中的操作</a></td>
</tr>
<tr class="even">
<td align="left">总线枚举</td>
<td align="left"><a href="enumerating-the-devices-on-a-bus.md" data-raw-source="[Enumerating the Devices on a Bus](enumerating-the-devices-on-a-bus.md)">枚举的总线上的设备</a></td>
</tr>
<tr class="odd">
<td align="left">（有限的支持是 UMDF 中提供） 的功能的电源状态</td>
<td align="left"><a href="supporting-functional-power-states.md" data-raw-source="[Supporting Functional Power States](supporting-functional-power-states.md)">支持功能的电源状态</a></td>
</tr>
<tr class="even">
<td align="left">WDM 对象和 Irp 访问</td>
<td align="left"><a href="obtaining-wdm-information.md" data-raw-source="[Obtaining WDM Information](obtaining-wdm-information.md)">获取 WDM 信息</a></td>
</tr>
<tr class="odd">
<td align="left">既不缓冲，也不直接 I/O</td>
<td align="left"><p><a href="accessing-data-buffers-in-wdf-drivers.md#neither" data-raw-source="[Accessing Data Buffers in WDF Drivers](accessing-data-buffers-in-wdf-drivers.md#neither)">WDF 驱动程序中访问数据缓冲区</a></p>
<p><a href="managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue" data-raw-source="[Intercepting an I/O Request before it is Queued](managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue)">已排队之前截获 I/O 请求</a></p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context" data-raw-source="[&lt;em&gt;EvtIoInCallerContext&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)"><em>EvtIoInCallerContext</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left">内部设备控制请求 (Ioctl)</td>
<td align="left"><p><a href="sending-i-o-requests-synchronously.md" data-raw-source="[Sending I/O Requests Synchronously](sending-i-o-requests-synchronously.md)">以同步方式发送的 I/O 请求</a></p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></li>
</ul>
<p><a href="sending-i-o-requests-asynchronously.md" data-raw-source="[Sending I/O Requests Asynchronously](sending-i-o-requests-asynchronously.md)">以异步方式发送的 I/O 请求</a></p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">删除锁参加的 I/O 请求</td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetRemoveLockOptions&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions)"><strong>WdfDeviceInitSetRemoveLockOptions</strong></a></td>
</tr>
<tr class="even">
<td align="left">WMI</td>
<td align="left"><a href="introduction-to-wmi-for-kmdf-drivers.md" data-raw-source="[Introduction to WMI for KMDF Drivers](introduction-to-wmi-for-kmdf-drivers.md)">用于 KMDF 驱动程序的 WMI 简介</a></td>
</tr>
</tbody>
</table>

 

如果您的驱动程序不需要与上述任一情况，您可以编写 UMDF 2 而不是使用 KMDF 驱动程序。 由于这两个框架共享数目的接口，可更高版本到 KMDF 转换您的驱动程序，在需要时更新。 有关为什么你可能想要选择 UMDF 的信息，请参阅[优点的编写 UMDF 驱动程序](advantages-of-writing-umdf-drivers.md)。

有关 framework 对象以及由 KMDF 和 UMDF 支持的详细信息，请参阅[Framework 对象摘要](summary-of-framework-objects.md)。

显示所有的 Windows 驱动程序框架 (WDF) 回调方法和 framework 适用性的表格，请参阅[WDF 回调摘要和方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_wdf/)。

 

 





