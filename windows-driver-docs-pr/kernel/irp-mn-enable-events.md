---
title: IRP_MN_ENABLE_EVENTS
description: 注册一个或多个事件块的任何 WMI 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 35b95ba0-efd0-420a-abe0-664fc6311d02
keywords:
- IRP_MN_ENABLE_EVENTS 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: b7375b9531db59ff79dabeaedc987e336019358c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185159"
---
# <a name="irp_mn_enable_events"></a>IRP \_ MN \_ 启用 \_ 事件


注册一个或多个事件块的任何 WMI 驱动程序都必须处理此 IRP。 驱动程序可以通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 或处理 IRP 本身来处理 wmi irp，如 [处理 WMI 请求](./handling-wmi-requests.md)中所述。

如果驱动程序调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 来处理 **IRP \_ MN \_ ENABLE \_ EVENTS** 请求，则 WMI 反过来会调用该驱动程序的 [*DpWmiFunctionControl*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback) 例程。

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ 系统 \_ 控件**](irp-mj-system-control.md)

<a name="when-sent"></a>发送时间
---------

WMI 发送此 IRP，通知驱动程序数据使用者已请求事件的通知。

WMI \_ 在任意线程上下文中以 IRQL = 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId** 指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径** 指向标识要启用的事件块的 GUID。

WNODE**指示非**分页缓冲区的大小（在**参数.**) 中，该缓冲区必须大于或等于**sizeof** (的** \_ 标头**。 不注册跟踪块 (WMIREG \_ 标志 \_ 跟踪 GUID) 的驱动程序 \_ 可以忽略此参数。

**Parameters.WMI.Buffer** **WNODE \_ 标头**指示是否应跟踪事件 (WMI \_ 标志 \_ 跟踪 \_ GUID) 并提供系统记录器的句柄。 不注册跟踪块 (WMIREG \_ 标志 \_ 跟踪 GUID) 的驱动程序 \_ 可以忽略此参数。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/o 状态块


如果驱动程序通过调用[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp- &gt; IoStatus**和**irp- &gt; IoStatus。**

否则，驱动程序会将 **Irp- &gt; IoStatus** 设置为状态 \_ 成功，或设置为适当的错误状态，如下所示：

\_ \_ \_ 找不到 WMI \_ GUID 状态

状态 \_ 无效的 \_ 设备 \_ 请求

成功时，驱动程序将 **Irp- &gt; IoStatus** 设置为零。

<a name="operation"></a>操作
---------

驱动程序可以通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 或处理 IRP 本身来处理 wmi irp，如 [处理 WMI 请求](./handling-wmi-requests.md)中所述。

如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的 [*DpWmiFunctionControl*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback) 例程，或在 \_ 驱动程序未定义例程时返回状态 SUCCESS。

如果驱动程序处理 **IRP \_ MN \_ ENABLE \_ EVENTS** 请求本身，则只应在 **参数. ProviderId** 指向与驱动程序传递给 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的指针相同的设备对象时才执行此操作。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

驱动程序处理请求之前，应确定 **数据路径** 是否指向驱动程序支持的 GUID。 如果不是，则驱动程序必须失败 IRP 并返回 \_ 状态 \_ WMI \_ GUID \_ 找不到。

如果驱动程序支持事件块，它将为该数据块的所有实例启用该事件。

驱动程序无需检查是否已为事件块启用了事件，因为 WMI 会在第一个数据使用者启用事件时发送单个请求以启用事件块。 如果没有干预禁用请求，WMI 将不会发送要启用的另一个请求。

注册跟踪块 (WMIREG \_ 标志 \_ 跟踪 GUID) 的驱动程序 \_ 还必须确定是将该事件发送到 WMI 还是将事件发送到系统记录器进行跟踪。 如果请求了跟踪，则 **参数. Buffer** 将指向 [**WNODE \_ 标头**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header) 结构 **，其中使用** WNODE \_ 标志 \_ 跟踪 \_ GUID 和 **HistoricalContext** 包含记录器的句柄。

有关定义事件块、发送事件和跟踪的详细信息，请参阅 [Windows Management Instrumentation](./implementing-wmi.md)。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DpWmiFunctionControl*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP \_ MN \_ 禁用 \_ 事件**](irp-mn-disable-events.md)

[**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE \_ 事件 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item)

[**WNODE \_ 标头**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)

 

