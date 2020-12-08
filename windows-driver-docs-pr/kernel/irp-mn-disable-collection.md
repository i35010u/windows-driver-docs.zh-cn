---
title: IRP_MN_DISABLE_COLLECTION
description: 注册一个或多个数据块的任何 WMI 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
keywords:
- IRP_MN_DISABLE_COLLECTION Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: db703d35d3738b622ccebe7505a8994998c88a18
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783897"
---
# <a name="irp_mn_disable_collection"></a>IRP \_ MN \_ 禁用 \_ 收集


注册一个或多个数据块的任何 WMI 驱动程序都必须处理此 IRP。 驱动程序可以通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 或处理 IRP 本身来处理 wmi irp，如 [处理 WMI 请求](./handling-wmi-requests.md)中所述。

如果驱动程序调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 来处理 **IRP \_ MN \_ DISABLE \_ COLLECTION** 请求，则 WMI 反过来会调用该驱动程序的 [*DpWmiFunctionControl*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback) 例程。

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ 系统 \_ 控件**](irp-mj-system-control.md)

<a name="when-sent"></a>发送时间
---------

WMI 将发送此 IRP，请求驱动程序停止数据块的累积数据，该数据块的驱动程序已注册为收集开销较高且已启用数据收集。

WMI \_ 在任意线程上下文中以 IRQL = 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId** 指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径** 指向一个 GUID，该 GUID 标识应停止其数据累积的数据块。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/o 状态块


如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置 **irp- &gt; IoStatus** 和 **irp- &gt; IoStatus。**

否则，驱动程序会将 **Irp- &gt; IoStatus** 设置为状态 \_ 成功，或设置为适当的错误状态，如下所示：

\_ \_ \_ 找不到 WMI \_ GUID 状态

状态 \_ 无效的 \_ 设备 \_ 请求

成功时，驱动程序将 **Irp- &gt; IoStatus** 设置为零。

<a name="operation"></a>操作
---------

驱动程序通过在 \_ \_ [**WMIREGGUID**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)或 [**WMIGUIDREGINFO**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)结构（当驱动程序在注册或更新数据块时将其传递到 WMI）的 **Flags** 成员中设置 WMIREG 标志来注册数据块，从而导致收集成本高昂。 驱动程序无需为此类块累积数据，直到收到显式请求来启用收集。

如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的 [*DpWmiFunctionControl*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback) 例程，或在 \_ 驱动程序未定义例程时返回状态 SUCCESS。

如果驱动程序处理 **IRP \_ MN \_ DISABLE \_ COLLECTION** 请求本身，只应在 **参数. ProviderId** 指向与驱动程序传递给 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的指针相同的设备对象时才执行此操作。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

在处理请求之前，驱动程序必须确定 **数据路径** 是否指向驱动程序支持的 GUID。 如果不是，则驱动程序必须失败 IRP 并返回 \_ 状态 \_ WMI \_ GUID \_ 找不到。 如果数据块有效但未使用 WMIREG 标志进行注册 \_ \_ ，则驱动程序可能返回状态 " \_ 成功" 并不执行任何其他操作。

驱动程序不需要检查是否已禁用数据收集，因为当最后一个数据使用者禁用该数据块的收集时，WMI 将为该数据块发送单个禁用请求。 WMI 将不会发送其他禁用请求，而不会发出要启用的请求。

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

## <a name="see-also"></a>请参阅


[*DpWmiFunctionControl*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP \_ MN \_ 启用 \_ 收集**](irp-mn-enable-collection.md)

[**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WMIREGGUID**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)

[**WMIGUIDREGINFO**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)

[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

 

