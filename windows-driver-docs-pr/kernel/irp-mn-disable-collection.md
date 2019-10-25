---
title: IRP_MN_DISABLE_COLLECTION
description: 注册一个或多个数据块的任何 WMI 驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: de375d56-880e-4534-acab-8d0685f45ebe
keywords:
- IRP_MN_DISABLE_COLLECTION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 86c0c0faeabb963dda0b9ed8aa7ed11232e582fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828055"
---
# <a name="irp_mn_disable_collection"></a>IRP\_MN\_禁用\_集合


注册一个或多个数据块的任何 WMI 驱动程序都必须处理此 IRP。 驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理**IRP\_MN\_禁用\_集合**请求，则 WMI 反过来会调用该驱动程序的[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)发送时间
---------

WMI 将发送此 IRP，请求驱动程序停止数据块的累积数据，该数据块的驱动程序已注册为收集开销较高且已启用数据收集。

WMI 在任意线程上下文中以 IRQL = 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId**指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径**指向一个 GUID，该 GUID 标识应停止其数据累积的数据块。

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

驱动程序通过设置 WMIREG\_标志来注册数据块，这是在驱动程序注册或更新时驱动程序传递给 WMI 的[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)或[**WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)结构的**FLAGS**成员中\_开销高昂的数据块。 驱动程序无需为此类块累积数据，直到收到显式请求来启用收集。

如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)例程，或在驱动程序未定义例程的情况下返回状态\_成功。

如果驱动程序处理**IRP\_MN\_禁用\_集合**请求，则只有当**参数. ProviderId**指向与驱动程序传递到[**的指针相同的设备对象时，才应执行此操作。IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

在处理请求之前，驱动程序必须确定**数据路径**是否指向驱动程序支持的 GUID。 否则，驱动程序必须失败 IRP 并返回状态\_WMI\_GUID\_找不到\_。 如果数据块有效但未使用 WMIREG 注册\_标志开销较高\_，驱动程序可能返回状态\_成功，无需进一步操作。

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
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DpWmiFunctionControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_function_control_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**IRP\_MN\_启用\_收集**](irp-mn-enable-collection.md)

[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)

[**WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

 

 




