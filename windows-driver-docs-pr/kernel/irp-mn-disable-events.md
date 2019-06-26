---
title: IRP_MN_DISABLE_EVENTS
description: 注册一个或多个事件块任何 WMI 驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 3187643b-27d7-4a6d-8fbe-4f8eb6c251ed
keywords:
- IRP_MN_DISABLE_EVENTS Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: ebd4f27cc59882d0405fa28f2a2aacaefc2f7cfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383320"
---
# <a name="irpmndisableevents"></a>IRP\_MN\_DISABLE\_EVENTS


注册一个或多个事件块任何 WMI 驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)处理**IRP\_MN\_禁用\_事件**请求时，WMI 反过来调用驱动程序的[ *DpWmiFunctionControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_function_control_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将发送此 IRP 来通知该驱动程序的数据使用者已请求事件的任何进一步的通知。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**指向标识要禁用的事件块的 GUID。

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

如果驱动程序处理**IRP\_MN\_禁用\_事件**请求本身，才应该这样做**Parameters.WMI.ProviderId**指向同一个设备对象与指针，该驱动程序传递给[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

之前处理请求，该驱动程序必须确定是否**Parameters.WMI.DataPath**指向 GUID 的驱动程序支持。 如果不是，该驱动程序必须失败 IRP，并返回状态\_WMI\_GUID\_不\_找到。

如果该驱动程序支持事件块，它将禁用该块中的所有实例的事件。

不需要的驱动程序来检查因为 WMI 当最后一个数据使用者禁用事件时发送该事件块的单个禁用请求是否事件的事件块已被禁用。 WMI 不会发送另一个没有启用的干预请求禁用请求。

有关事件块定义的详细信息，请参阅[设计 WMI 数据和事件块](https://docs.microsoft.com/windows-hardware/drivers/kernel/designing-wmi-data-and-event-blocks)。

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

[**IRP\_MN\_ENABLE\_EVENTS**](irp-mn-enable-events.md)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

 

 




