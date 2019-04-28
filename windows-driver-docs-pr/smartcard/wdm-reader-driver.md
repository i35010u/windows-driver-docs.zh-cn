---
title: WDM 读卡器驱动程序
description: WDM 读卡器驱动程序
ms.assetid: ead76f5f-1d28-4343-99c0-e7974fa4c3da
keywords:
- 供应商提供的驱动程序 WDK 的智能卡、 所需的例程
- WDM WDK 智能卡
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a5ed983d3e32e4491d965624726e9cadf070512
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348118"
---
# <a name="wdm-reader-driver"></a>WDM 读卡器驱动程序


## <span id="_ntovr_wdm_reader_driver"></span><span id="_NTOVR_WDM_READER_DRIVER"></span>


下表列出了所需的 WDM 读卡器驱动程序的例程。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544113" data-raw-source="[&lt;strong&gt;DriverEntry&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544113)"><strong>DriverEntry</strong></a></p></td>
<td align="left"><p>初始化的驱动程序对象和调度表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"><em>AddDevice</em></a></p></td>
<td align="left"><p>为智能卡读卡器中创建设备对象。 此外， <a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"> <em>AddDevice</em> </a>可以调用任意以下驱动程序库例程：</p>
<ul>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548944" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548944)"><strong>SmartcardInitialize (WDM)</strong> </a>完成驱动程序初始化。 调用该例程<a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"> <em>AddDevice</em> </a>是强制性。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548947" data-raw-source="[&lt;strong&gt;SmartcardLogError (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548947)"><strong>SmartcardLogError (WDM)</strong> </a>来记录错误。 驱动程序必须调用此例程<a href="https://msdn.microsoft.com/library/windows/hardware/ff540521" data-raw-source="[&lt;em&gt;AddDevice&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540521)"> <em>AddDevice</em> </a>如果<a href="https://msdn.microsoft.com/library/windows/hardware/ff548944" data-raw-source="[&lt;strong&gt;SmartcardInitialize (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548944)"> <strong>SmartcardInitialize (WDM)</strong> </a>失败。</p></li>
<li><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548935" data-raw-source="[&lt;strong&gt;SmartcardCreateLink (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548935)"><strong>SmartcardCreateLink (WDM)</strong> </a>在注册表中创建符号读取器设备的链接。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564886" data-raw-source="[&lt;em&gt;Unload&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564886)"><em>卸载</em></a></p></td>
<td align="left"><p>从系统中删除驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff543266" data-raw-source="[&lt;em&gt;DispatchCreate&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff543266)"><em>DispatchCreate</em></a></p>
<p>-和-</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchClose&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchClose</em></a></p></td>
<td align="left"><p>支持<a href="https://msdn.microsoft.com/library/windows/hardware/ff550729" data-raw-source="[&lt;strong&gt;IRP_MJ_CREATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550729)"> <strong>IRP_MJ_CREATE</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff550720" data-raw-source="[&lt;strong&gt;IRP_MJ_CLOSE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550720)"> <strong>IRP_MJ_CLOSE</strong></a>分别。 若要建立与读取器的连接，资源管理器将发送<strong>IRP_MJ_CREATE</strong>到读卡器驱动程序。 若要断开的连接，资源管理器将发送<strong>IRP_MJ_CLOSE</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchCleanup&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchCleanup</em></a></p></td>
<td align="left"><p>支持<a href="https://msdn.microsoft.com/library/windows/hardware/ff550718" data-raw-source="[&lt;strong&gt;IRP_MJ_CLEANUP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550718)"> <strong>IRP_MJ_CLEANUP</strong></a>，用于资源管理器将发送到读卡器驱动程序取消挂起的 I/O 请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPnP&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchPnP</em></a></p></td>
<td align="left"><p>支持<a href="https://msdn.microsoft.com/library/windows/hardware/ff550772" data-raw-source="[&lt;strong&gt;IRP_MJ_PNP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550772)"> <strong>IRP_MJ_PNP</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchPower&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchPower</em></a></p></td>
<td align="left"><p>支持<a href="https://msdn.microsoft.com/library/windows/hardware/ff550784" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550784)"> <strong>IRP_MJ_POWER</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"><em>DispatchDeviceControl</em></a></p></td>
<td align="left"><p>支持<a href="https://msdn.microsoft.com/library/windows/hardware/ff550744" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550744)"> <strong>IRP_MJ_DEVICE_CONTROL</strong> </a>和是智能卡请求的主入口点。 在收到 IRP_MJ_DEVICE_CONTROL 后, <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch" data-raw-source="[&lt;em&gt;DispatchDeviceControl&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)"> <em>DispatchDeviceControl</em> </a>必须立即调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff548939" data-raw-source="[&lt;strong&gt;SmartcardDeviceControl (WDM)&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548939)"> <strong>SmartcardDeviceControl (WDM)</strong></a>，这是处理设备控制请求的智能卡驱动程序库例程。 下面的代码示例演示如何从 WDM 驱动程序调用此库例程：</p>
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
<p>如果无法处理在调用中，指示特定 IOCTL <strong>SmartcardDeviceControl</strong>将未知 IOCTL 请求调用驱动程序的回调。</p></td>
</tr>
</tbody>
</table>

 

 

 





