---
title: WDM 读卡器驱动程序
description: WDM 读卡器驱动程序
ms.assetid: ead76f5f-1d28-4343-99c0-e7974fa4c3da
keywords:
- 供应商提供的驱动程序 WDK 智能卡，必需例程
- WDM WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 191d39bc0cca370677add795636a09328d9ad75a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842613"
---
# <a name="wdm-reader-driver"></a>WDM 读卡器驱动程序


## <span id="_ntovr_wdm_reader_driver"></span><span id="_NTOVR_WDM_READER_DRIVER"></span>


下表列出了 WDM 读取器驱动程序所需的例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)"><strong>DriverEntry</strong></a></p></td>
<td align="left"><p>初始化驱动程序对象和调度表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a></p></td>
<td align="left"><p>创建智能卡读卡器的设备对象。 此外， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a>可以调用以下任何驱动程序库例程：</p>
<ul>
<li><p><a href="https://docs.microsoft.com/previous-versions/ff548944(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548944(v=vs.85))"><strong>SmartcardInitialize （WDM）</strong></a>来完成驱动程序初始化。 在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a>中调用此例程为必备。</p></li>
<li><p><a href="https://docs.microsoft.com/previous-versions/ff548947(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardLogError (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548947(v=vs.85))"><strong>SmartcardLogError （WDM）</strong></a>记录一个错误。 如果<a href="https://docs.microsoft.com/previous-versions/ff548944(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548944(v=vs.85))"><strong>SmartcardInitialize （WDM）</strong></a>失败，则驱动程序必须在<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)"><em>AddDevice</em></a>中调用此例程。</p></li>
<li><p><a href="https://docs.microsoft.com/previous-versions/ff548935(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardCreateLink (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548935(v=vs.85))"><strong>SmartcardCreateLink （WDM）</strong></a>为注册表中的读取器设备创建一个符号链接。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload)"></a></p></td>
<td align="left"><p>从系统中删除驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543266" data-raw-source="[&lt;em&gt;DispatchCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543266)"><em>DispatchCreate</em></a></p>
<p>-和-</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchClose&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchClose</em></a></p></td>
<td align="left"><p>分别支持<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create)"><strong>IRP_MJ_CREATE</strong></a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)"><strong>IRP_MJ_CLOSE</strong></a>。 为了与读取器建立连接，资源管理器会将<strong>IRP_MJ_CREATE</strong>发送到读取器驱动程序。 若要连接到服务器，资源管理器将发送<strong>IRP_MJ_CLOSE</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchCleanup</em></a></p></td>
<td align="left"><p>支持<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-cleanup)"><strong>IRP_MJ_CLEANUP</strong></a>，资源管理器会将其发送到读取器驱动程序以取消挂起的 i/o 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPnP&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPnP</em></a></p></td>
<td align="left"><p>支持<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp)"><strong>IRP_MJ_PNP</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a></p></td>
<td align="left"><p>支持<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchDeviceControl</em></a></p></td>
<td align="left"><p>支持<a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a> ，是智能卡请求的主要入口点。 接收到 IRP_MJ_DEVICE_CONTROL 后， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)"><em>DispatchDeviceControl</em></a>必须立即调用<a href="https://docs.microsoft.com/previous-versions/ff548939(v=vs.85)" data-raw-source="[&lt;strong&gt;SmartcardDeviceControl (WDM)&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))"><strong>SmartcardDeviceControl （WDM）</strong></a>，这是处理设备控制请求的智能卡驱动程序库例程。 下面的代码示例演示如何从 WDM 驱动程序调用此库例程：</p>
<pre space="preserve"><code>NTSTATUS
DriverDeviceControl(
    PDEVICE_OBJECT DeviceObject,
    PIRP Irp
    )
{
    PDEVICE_EXTENSION deviceExtension = DeviceObject -&gt; DeviceExtension;

    return SmartcardDeviceControl(
        &(deviceExtension-&gt;SmartcardExtension),
        Irp
        );
}</code></pre>
<p>如果无法处理在调用中指定的特定 IOCTL， <strong>SmartcardDeviceControl</strong>将调用驱动程序对未知 IOCTL 请求的回调。</p></td>
</tr>
</tbody>
</table>

 

 

 





