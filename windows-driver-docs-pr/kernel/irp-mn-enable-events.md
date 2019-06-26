---
title: IRP_MN_ENABLE_EVENTS
description: 注册一个或多个事件块任何 WMI 驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 35b95ba0-efd0-420a-abe0-664fc6311d02
keywords:
- IRP_MN_ENABLE_EVENTS Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 84874bbd689040f0580393ce0f79b59317775eed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353368"
---
# <a name="irpmnenableevents"></a>IRP\_MN\_ENABLE\_EVENTS


注册一个或多个事件块任何 WMI 驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)处理**IRP\_MN\_启用\_事件**请求时，WMI 反过来调用驱动程序的[ *DpWmiFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将发送此 IRP 来通知该驱动程序的数据使用者已请求事件的通知。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**指向标识要启用的事件块的 GUID。

**Parameters.WMI.BufferSize**指示在非分页缓冲区的大小**Parameters.WMI.Buffer**，它必须是大于或等于**sizeof**(**WNODE\_标头**)。 不会注册跟踪块的驱动程序 (WMIREG\_标志\_跟踪\_GUID) 可以忽略此参数。

**Parameters.WMI.Buffer**指向**WNODE\_标头**，该值指示是否应跟踪的事件 (WMI\_标志\_跟踪\_GUID)，并提供一个句柄到系统记录器。 不会注册跟踪块的驱动程序 (WMIREG\_标志\_跟踪\_GUID) 可以忽略此参数。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_WMI\_GUID\_不\_找到

STATUS\_INVALID\_DEVICE\_REQUEST

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**为零。

<a name="operation"></a>操作
---------

驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，例程调用的驱动程序[ *DpWmiFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)例程，返回状态或\_成功如果驱动程序不会定义该例程。

如果驱动程序处理**IRP\_MN\_启用\_事件**请求本身，才应该这样做**Parameters.WMI.ProviderId**指向与相同的设备对象该驱动程序传递到指针[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

该驱动程序处理请求之前，它应该确定是否**Parameters.WMI.DataPath**指向该驱动程序支持的 GUID。 如果不是，该驱动程序必须失败 IRP，并返回状态\_WMI\_GUID\_不\_找到。

如果该驱动程序支持事件块，它将启用该数据块的所有实例的事件。

不需要的驱动程序来检查是否已启用事件的事件块因为 WMI 将发送一个请求，若要启用用于事件块，当第一个数据使用者启用该事件。 WMI 不会发送另一个请求以启用无有干预性禁用请求。

注册跟踪块的驱动程序 (WMIREG\_标志\_跟踪\_GUID) 还必须确定是否要将事件发送到 WMI 或跟踪系统记录器。 如果请求跟踪，则**Parameters.WMI.Buffer**指向[ **WNODE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-_wnode_header)结构在其中**标志**是设置与 WNODE\_标志\_跟踪\_GUID 和**HistoricalContext**包含记录器的句柄。

有关事件块定义的详细信息，发送事件和跟踪，请参阅[Windows Management Instrumentation](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-wmi)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP\_MN\_DISABLE\_EVENTS**](irp-mn-disable-events.md)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_EVENT\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_event_item)

[**WNODE\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-_wnode_header)

 

 




