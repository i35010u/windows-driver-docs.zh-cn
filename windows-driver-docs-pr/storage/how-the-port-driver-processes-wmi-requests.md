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
ms.openlocfilehash: 52b34b9fd955e4f4a181ceeebb326386a816f18a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385949"
---
# <a name="how-the-port-driver-processes-wmi-requests"></a>端口驱动程序如何处理 WMI 请求


## <span id="ddk_how_the_port_driver_processes_wmi_requests_kg"></span><span id="DDK_HOW_THE_PORT_DRIVER_PROCESSES_WMI_REQUESTS_KG"></span>


Windows 会通过发送 I/O 请求数据包 (IRP) 类型的通知的 WMI 请求存储端口驱动程序[ **IRP\_MJ\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)中所述，[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)。 系统控制 IRP 可以包含任何次要 IRP 数字表示 WMI 操作。 有关详细信息，请参阅[WMI 次要 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)"><strong>IRP_MN_REGINFO</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryReginfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)"><strong>HwScsiWmiQueryReginfo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiSetDataBlock</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem" data-raw-source="[&lt;strong&gt;HwScsiWmiSetDataItem&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)"><strong>HwScsiWmiSetDataItem</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method" data-raw-source="[&lt;strong&gt;HwScsiWmiExecuteMethod&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)"><strong>HwScsiWmiExecuteMethod</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_EVENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-events)"><strong>IRP_MN_ENABLE_EVENTS</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control" data-raw-source="[&lt;strong&gt;HwScsiWmiFunctionControl&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)"><strong>HwScsiWmiFunctionControl</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_EVENTS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-events)"><strong>IRP_MN_DISABLE_EVENTS</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_COLLECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)"><strong>IRP_MN_ENABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_COLLECTION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)"><strong>IRP_MN_DISABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
</tbody>
</table>

 

每个微型端口驱动程序回调例程应提供与相应的 WMI 次要 IRP 相关的功能数或数字。 一些例程，如*HwScsiWmiFunctionControl*，必须能够提供给多个 WMI 次要 IRP 编号对应的功能。

微型端口驱动程序将调用 SCSI 端口 WMI 库调度例程[ **ScsiPortWmiDispatchFunction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)，然后调度例程将调用相应的微型端口驱动程序回调例程。 端口驱动程序将 WMI 次 IRP 版本号传输到 SRB 以便调度例程，请查阅 SRB 来确定要调用的回调例程。

下图说明了 WMI 请求将从存储端口驱动程序存储微型端口驱动程序将其传递给 SCSI 端口 WMI 库调度例程之前接收的那一刻起进行的更改。

![如何存储堆栈处理 wmi irp ](images/scsiwmilib.png)

1.  以下步骤说明如何存储堆栈会重新打包为 SRB WMI IRP:

2.  Windows 通知的 WMI 请求存储端口驱动程序通过发送类型的 IRP [ **IRP\_MJ\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)。

3.  端口驱动程序重新打包为类型 WMI SRB WMI IRP [ **SCSIWMI\_请求\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiwmi/ns-scsiwmi-scsiwmi_request_context) ，并将分配的值为 SRB\_函数\_到 WMISRB**函数**成员。 端口驱动程序将次 WMI IRP 版本号传输到 SRB **WMISubFunction**成员。 和安排 I/O manager 能够调用微型端口驱动程序的启动 I/O 例程[ **HwScsiStartIo** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557323(v=vs.85))通过调用[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket).

4.  微型端口驱动程序调用 SCSI 端口 WMI 库调度例程来处理 SRB。 有关详细信息，请参阅[使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)。

 

 




