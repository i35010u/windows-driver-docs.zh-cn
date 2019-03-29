---
title: 端口驱动程序如何处理 WMI 请求
description: 端口驱动程序如何处理 WMI 请求
ms.assetid: 0b56d382-3c4b-4192-be49-3bad50b0a0ed
keywords:
- WMI Srb WDK 存储，WMI 请求处理
- 回调例程 WDK WMI Srb
- WMI Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea9f9bb0f6507048ee21111a68fb669b7431125
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562592"
---
# <a name="how-the-port-driver-processes-wmi-requests"></a>端口驱动程序如何处理 WMI 请求


## <span id="ddk_how_the_port_driver_processes_wmi_requests_kg"></span><span id="DDK_HOW_THE_PORT_DRIVER_PROCESSES_WMI_REQUESTS_KG"></span>


Windows 会通过发送 I/O 请求数据包 (IRP) 类型的通知的 WMI 请求存储端口驱动程序[ **IRP\_MJ\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550813)中所述，[Windows Management Instrumentation](https://msdn.microsoft.com/library/windows/hardware/ff547139)。 系统控制 IRP 可以包含任何次要 IRP 数字表示 WMI 操作。 有关详细信息，请参阅[WMI 次要 Irp](https://msdn.microsoft.com/library/windows/hardware/ff566361)。

若要使用[使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)处理 WMI Srb，SCSI 微型端口驱动程序必须提供一系列相对应的回调例程到 WMI 次要 IRP 编号。 下表说明了微型端口驱动程序回调例程和其相应的 WMI 次要 IRP 编号之间的关系。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WMI IRP 次版本号</th>
<th align="left">微型端口驱动程序回调例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551731" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551731)"><strong>IRP_MN_REGINFO</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557344" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryReginfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557344)"><strong>HwScsiWmiQueryReginfo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551650" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551650)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557340" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557340)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551718" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551718)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557340" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557340)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550831" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550831)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiSetDataBlock</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550836" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550836)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557357" data-raw-source="[&lt;strong&gt;HwScsiWmiSetDataItem&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557357)"><strong>HwScsiWmiSetDataItem</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550868" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550868)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557332" data-raw-source="[&lt;strong&gt;HwScsiWmiExecuteMethod&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557332)"><strong>HwScsiWmiExecuteMethod</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550859" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_EVENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550859)"><strong>IRP_MN_ENABLE_EVENTS</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557338" data-raw-source="[&lt;strong&gt;HwScsiWmiFunctionControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557338)"><strong>HwScsiWmiFunctionControl</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550851" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_EVENTS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550851)"><strong>IRP_MN_DISABLE_EVENTS</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550857" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_COLLECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550857)"><strong>IRP_MN_ENABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550848" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_COLLECTION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550848)"><strong>IRP_MN_DISABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
</tbody>
</table>

 

每个微型端口驱动程序回调例程应提供与相应的 WMI 次要 IRP 相关的功能数或数字。 一些例程，如*HwScsiWmiFunctionControl*，必须能够提供给多个 WMI 次要 IRP 编号对应的功能。

微型端口驱动程序将调用 SCSI 端口 WMI 库调度例程[ **ScsiPortWmiDispatchFunction**](https://msdn.microsoft.com/library/windows/hardware/ff564766)，然后调度例程将调用相应的微型端口驱动程序回调例程。 端口驱动程序将 WMI 次 IRP 版本号传输到 SRB 以便调度例程，请查阅 SRB 来确定要调用的回调例程。

下图说明了 WMI 请求将从存储端口驱动程序存储微型端口驱动程序将其传递给 SCSI 端口 WMI 库调度例程之前接收的那一刻起进行的更改。

![如何存储堆栈处理 wmi irp ](images/scsiwmilib.png)

1.  以下步骤说明如何存储堆栈会重新打包为 SRB WMI IRP:

2.  Windows 通知的 WMI 请求存储端口驱动程序通过发送类型的 IRP [ **IRP\_MJ\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550813)。

3.  端口驱动程序重新打包为类型 WMI SRB WMI IRP [ **SCSIWMI\_请求\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff564946) ，并将分配的值为 SRB\_函数\_到 WMISRB**函数**成员。 端口驱动程序将次 WMI IRP 版本号传输到 SRB **WMISubFunction**成员。 和安排 I/O manager 能够调用微型端口驱动程序的启动 I/O 例程[ **HwScsiStartIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557323)通过调用[ **IoStartPacket** ](https://msdn.microsoft.com/library/windows/hardware/ff550370).

4.  微型端口驱动程序调用 SCSI 端口 WMI 库调度例程来处理 SRB。 有关详细信息，请参阅[使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)。

 

 




