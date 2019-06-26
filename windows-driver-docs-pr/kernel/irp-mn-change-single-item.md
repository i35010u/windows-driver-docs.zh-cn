---
title: IRP_MN_CHANGE_SINGLE_ITEM
description: 支持 WMI 的所有驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 9839ebb2-31a9-4cb0-adbf-1882583849fc
keywords:
- IRP_MN_CHANGE_SINGLE_ITEM 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 33a91f80058f3c5f75fd597aacb125c30d3ed9a5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382240"
---
# <a name="irpmnchangesingleitem"></a>IRP\_MN\_更改\_单个\_项


支持 WMI 的所有驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)处理**IRP\_MN\_更改\_单一\_项**请求，WMI 又会调用该驱动程序[ *DpWmiSetDataItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将发送此 IRP，若要更改一个数据块的单个实例中的数据项。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**指向标识要设置的数据块的 GUID。

**Parameters.WMI.BufferSize**指示在非分页缓冲区的大小**Parameters.WMI.Buffer**。

**Parameters.WMI.Buffer**，指向[ **WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)标识数据的实例结构块，若要设置，项的 ID 和一个新数据值。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_WMI\_实例\_不\_找到

状态\_WMI\_ITEMID\_不\_找到

状态\_WMI\_GUID\_不\_找到

状态\_WMI\_读取\_仅

状态\_WMI\_设置\_失败

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**为零。

<a name="operation"></a>操作
---------

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，例程调用的驱动程序[ *DpWmiSetDataItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)例程，或返回状态\_WMI\_读取\_仅当驱动程序不会定义该例程。

如果驱动程序处理**IRP\_MN\_更改\_单个\_项**请求本身，才应该这样做**Parameters.WMI.ProviderId**指向与传递给驱动程序的指针相同的设备对象[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

未实现对支持**IRP\_MN\_更改\_单个\_项**除非你确信系统提供的用户模式组件需要此功能。

之前处理请求，该驱动程序必须确定是否**Parameters.WMI.DataPath**指向该驱动程序支持的 GUID。 如果未显示，该驱动程序必须失败 IRP，并且返回状态\_WMI\_GUID\_不\_找到。

如果该驱动程序支持的数据块，则必须检查输入[ **WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)结构**Parameters.WMI.Buffer**指向实例名称，如下所示：

-   如果 WNODE\_标志\_静态\_实例\_中设置的名称**WnodeHeader.Flags**，则驱动程序使用**InstanceIndex**作为中的索引为该块的静态实例名称的驱动程序的列表。 WMI 从注册块时，驱动程序提供的注册数据中获取索引。

-   如果 WNODE\_标志\_静态\_实例\_名称是明确**WnodeHeader.Flags，** 驱动程序使用的偏移量**OffsetInstanceName**到输入中找到的实例名称字符串[ **WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)结构。 **OffsetInstanceName**是从结构开始到 USHORT 大小以字节为单位 （而不是字符） 的实例名称字符串的长度的字节偏移量。 此长度包括整个 NULL 终止符如果存在后, 跟实例名称字符串，以 unicode 格式。

该驱动程序负责验证所有输入的值。 具体而言，如果处理 IRP 请求本身，则该驱动程序，就必须执行以下操作：

-   对于静态名称，请验证**InstanceIndex** WNODE 成员\_单个\_项结构位于范围内支持的数据块的驱动程序的实例索引。

-   有关动态名称，验证实例名称字符串标识驱动程序支持的数据块实例。

-   确认**ItemId**的成员[ **WNODE\_单一\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)结构是支持的项标识符的范围内数据块的驱动程序。

-   确认**DataBlockOffset**并**SizeDataItem**的成员**WNODE\_单一\_项**结构描述有效大小的数据块和缓冲区的内容是有效的数据项。

-   确保指定的数据项目是为其驱动程序允许调用方启动的修改。 换而言之，驱动程序不应允许对想要为只读的数据项的修改。

不要假定线程上下文是起始用户模式应用程序 — 更高级别的驱动程序可能已更改它。

如果该驱动程序找不到指定的实例，它必须失败 IRP，并返回状态\_WMI\_实例\_不\_找到。 对于使用动态实例名称的实例，此状态指示驱动程序不支持该实例。 因此，WMI 可以继续查询其他数据提供程序，并返回相应的错误数据使用者，如果另一个提供程序的实例，但由于某种原因无法处理该请求。

如果驱动程序查找该实例，并可以处理该请求，其数据中的项设置为中值的实例[ **WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)。 如果数据项是只读的该驱动程序会使项保持不变，失败 IRP，并返回状态\_WMI\_读取\_仅。

如果该实例有效，但该驱动程序无法处理请求，它可以返回任何相应的错误状态。

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


[*DpWmiSetDataItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_dataitem_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_item)

 

 




