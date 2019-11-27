---
title: IRP_MN_ENABLE_EVENTS
description: 注册一个或多个事件块的任何 WMI 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 35b95ba0-efd0-420a-abe0-664fc6311d02
keywords:
- IRP_MN_ENABLE_EVENTS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 0395173ac5d7b52f109d3b98ac55e345f7ea074b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838581"
---
# <a name="irp_mn_enable_events"></a>IRP\_MN\_启用\_事件


注册一个或多个事件块的任何 WMI 驱动程序都必须处理此 IRP。 驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理**IRP\_MN\_启用\_事件**请求，WMI 反过来会调用该驱动程序的[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)发送时间
---------

WMI 发送此 IRP，通知驱动程序数据使用者已请求事件的通知。

WMI 在任意线程上下文中以 IRQL = 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId**指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径**指向标识要启用的事件块的 GUID。

WNODE**指示非**分页缓冲区在**参数. buffer**的大小，该缓冲区必须大于或等于**SIZEOF**（ **\_标头**）。 不注册跟踪块的驱动程序（WMIREG\_标记\_跟踪\_GUID）可以忽略此参数。

WNODE 用于指示是否应跟踪事件 **（wmi\_** 标志\_跟踪\_GUID）并提供系统记录器的句柄的 **\_标头**。 不注册跟踪块的驱动程序（WMIREG\_标记\_跟踪\_GUID）可以忽略此参数。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp&gt;IoStatus**和**irp-&gt;IoStatus** 。

否则，驱动程序会将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS 或适当的错误状态，如下所示：

找不到\_WMI\_GUID\_的状态\_

状态\_无效\_设备\_请求

成功时，驱动程序将**Irp&gt;IoStatus**设置为零。

<a name="operation"></a>操作
---------

驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)例程，或在驱动程序未定义例程的情况下返回状态\_成功。

如果驱动程序处理**IRP\_MN\_启用\_事件**请求本身，则只有当 IoWMIRegistrationControl 指向的设备对象与驱动程序传递到[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的指针**相同时，** 才应执行此操作。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

驱动程序处理请求之前，应确定**数据路径**是否指向驱动程序支持的 GUID。 否则，驱动程序必须失败 IRP 并返回状态\_WMI\_GUID\_找不到\_。

如果驱动程序支持事件块，它将为该数据块的所有实例启用该事件。

驱动程序无需检查是否已为事件块启用了事件，因为 WMI 会在第一个数据使用者启用事件时发送单个请求以启用事件块。 如果没有干预禁用请求，WMI 将不会发送要启用的另一个请求。

注册跟踪块（WMIREG\_标志\_跟踪\_GUID）的驱动程序还必须确定是将事件发送到 WMI 还是将事件发送到系统记录器进行跟踪。 如果请求**跟踪，则**WNODE 会指向一个[ **\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)结构，其中使用 WNODE\_标志设置**标志**，\_跟踪\_GUID， **HistoricalContext**包含记录器.

有关定义事件块、发送事件和跟踪的详细信息，请参阅[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP\_MN\_禁用\_事件**](irp-mn-disable-events.md)

[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_事件\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item)

[**WNODE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)

 

 




