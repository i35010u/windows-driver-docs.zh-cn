---
title: 端口驱动程序如何处理 WMI 请求
description: 端口驱动程序如何处理 WMI 请求
ms.assetid: 0b56d382-3c4b-4192-be49-3bad50b0a0ed
keywords:
- WMI SRBs WDK 存储，WMI 请求处理
- 回调例程 WDK WMI SRBs
- WMI Irp WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6db08d92746dc2921eced52b44c548c2556c5e14
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105184"
---
# <a name="how-the-port-driver-processes-wmi-requests"></a>端口驱动程序如何处理 WMI 请求


## <span id="ddk_how_the_port_driver_processes_wmi_requests_kg"></span><span id="DDK_HOW_THE_PORT_DRIVER_PROCESSES_WMI_REQUESTS_KG"></span>


Windows 通过发送一个类型为 [**irp \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)的 i/o 请求数据包 (irp) 来通知 WMI 请求的存储端口驱动程序，如 [Windows Management Instrumentation](../kernel/implementing-wmi.md)中所述。 系统控制 IRP 可以包含任何表示 WMI 操作的次要 IRP 号码。 有关详细信息，请参阅 [WMI 次要 irp](../kernel/wmi-minor-irps.md)。

若要使用 [Scsi 端口 Wmi 库](using-the-scsi-port-wmi-library.md) 来处理 wmi SRBS，SCSI 微型端口驱动程序必须提供一系列与 WMI 次要 IRP 号对应的回调例程。 下表说明了微型端口驱动程序回调例程与其相应的 WMI 次要 IRP 号之间的关系。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">WMI IRP 次要版本号</th>
<th align="left">微型端口驱动程序回调例程</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-reginfo" data-raw-source="[&lt;strong&gt;IRP_MN_REGINFO&lt;/strong&gt;](../kernel/irp-mn-reginfo.md)"><strong>IRP_MN_REGINFO</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryReginfo&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_reginfo)"><strong>HwScsiWmiQueryReginfo</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-query-all-data" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](../kernel/irp-mn-query-all-data.md)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-query-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](../kernel/irp-mn-query-single-instance.md)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock" data-raw-source="[&lt;strong&gt;HwScsiWmiQueryDataBlock&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_query_datablock)"><strong>HwScsiWmiQueryDataBlock</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-change-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](../kernel/irp-mn-change-single-instance.md)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiSetDataBlock</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-change-single-item" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](../kernel/irp-mn-change-single-item.md)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem" data-raw-source="[&lt;strong&gt;HwScsiWmiSetDataItem&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_set_dataitem)"><strong>HwScsiWmiSetDataItem</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-execute-method" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](../kernel/irp-mn-execute-method.md)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method" data-raw-source="[&lt;strong&gt;HwScsiWmiExecuteMethod&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_execute_method)"><strong>HwScsiWmiExecuteMethod</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-enable-events" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_EVENTS&lt;/strong&gt;](../kernel/irp-mn-enable-events.md)"><strong>IRP_MN_ENABLE_EVENTS</strong></a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_function_control" data-raw-source="[&lt;strong&gt;HwScsiWmiFunctionControl&lt;/strong&gt;](/windows-hardware/drivers/ddi/scsiwmi/nc-scsiwmi-pscsiwmi_function_control)"><strong>HwScsiWmiFunctionControl</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-disable-events" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_EVENTS&lt;/strong&gt;](../kernel/irp-mn-disable-events.md)"><strong>IRP_MN_DISABLE_EVENTS</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-enable-collection" data-raw-source="[&lt;strong&gt;IRP_MN_ENABLE_COLLECTION&lt;/strong&gt;](../kernel/irp-mn-enable-collection.md)"><strong>IRP_MN_ENABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/kernel/irp-mn-disable-collection" data-raw-source="[&lt;strong&gt;IRP_MN_DISABLE_COLLECTION&lt;/strong&gt;](../kernel/irp-mn-disable-collection.md)"><strong>IRP_MN_DISABLE_COLLECTION</strong></a></p></td>
<td align="left"><p><em>HwScsiWmiFunctionControl</em></p></td>
</tr>
</tbody>
</table>

 

每个微型端口驱动程序回调例程都应该提供与相应 WMI 次要 IRP 号或数字相关联的功能。 某些例程（如 *HwScsiWmiFunctionControl*）必须能够提供与多个 WMI 次要 IRP 号对应的功能。

微型端口驱动程序将调用 SCSI 端口 WMI 库调度例程 [**ScsiPortWmiDispatchFunction**](/windows-hardware/drivers/ddi/scsiwmi/nf-scsiwmi-scsiportwmidispatchfunction)，然后调度例程将调用相应的微型端口驱动程序回调例程。 端口驱动程序将 WMI 次要 IRP 编号传输到 SRB，以便调度例程可以参考 SRB 来确定要调用的回调例程。

下图说明了 WMI 请求从存储端口驱动程序接收到的时间到存储微型端口驱动程序将其传递到 SCSI 端口 WMI 库调度例程之前所经历的更改。

![存储堆栈如何处理 wmi irp ](images/scsiwmilib.png)

1.  以下步骤说明了存储堆栈如何将 WMI IRP 重新打包为 SRB：

2.  Windows 通过发送 [**irp \_ MJ \_ 系统 \_ 控件**](../kernel/irp-mj-system-control.md)的 irp 通知 WMI 请求的存储端口驱动程序。

3.  端口驱动程序将 WMI IRP 重新打包为 [**SCSIWMI \_ 请求 \_ 上下文**](/windows-hardware/drivers/ddi/scsiwmi/ns-scsiwmi-scsiwmi_request_context) 类型的 wmi SRB，并将 SRB 函数 WMI 的值分配 \_ \_ 给 SRB 的 **函数** 成员。 端口驱动程序将次要 WMI IRP 号传输到 SRB **WMISubFunction** 成员。 并安排 i/o 管理器通过调用[**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)调用微型端口驱动程序的启动 I/o 例程[**HwScsiStartIo**](/previous-versions/windows/hardware/drivers/ff557323(v=vs.85)) 。

4.  微型端口驱动程序调用 SCSI 端口 WMI 库调度例程来处理 SRB。 有关详细信息，请参阅 [使用 SCSI 端口 WMI 库](using-the-scsi-port-wmi-library.md)。

