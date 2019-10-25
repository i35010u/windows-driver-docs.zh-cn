---
title: IRP_MN_CHANGE_SINGLE_ITEM
description: 支持 WMI 的所有驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 9839ebb2-31a9-4cb0-adbf-1882583849fc
keywords:
- IRP_MN_CHANGE_SINGLE_ITEM 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: b441da63c6f388f8541c7f77249c05dfb485df1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838592"
---
# <a name="irp_mn_change_single_item"></a>IRP\_MN\_更改\_单一\_项


支持 WMI 的所有驱动程序都必须处理此 IRP。 驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理**IRP\_MN\_更改\_单一\_项**请求，则 WMI 反过来会调用该驱动程序的[*DpWmiSetDataItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)发送时间
---------

WMI 发送此 IRP 以更改数据块的单个实例中的单个数据项。

WMI 在任意线程上下文中以 IRQL = 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId**指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径**指向标识要设置的数据块的 GUID。

**参数. BufferSize**指示非分页缓冲区在**参数. buffer**的大小。

然后，指向[**WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)**结构，该**结构标识数据块的实例、要设置的项的 ID 和新的数据值。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp&gt;IoStatus**和**irp-&gt;IoStatus** 。

否则，驱动程序会将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS 或适当的错误状态，如下所示：

找不到\_WMI\_实例的状态\_\_

\_\_WMI ITEMID\_找不到\_

找不到\_WMI\_GUID\_的状态\_

状态\_WMI\_仅读取\_

\_WMI\_集\_故障状态

成功时，驱动程序将**Irp&gt;IoStatus**设置为零。

<a name="operation"></a>操作
---------

如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的[*DpWmiSetDataItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)例程，或仅当驱动程序未定义例程时才\_读取\_的\_状态。

如果驱动程序处理**IRP\_MN\_更改\_单一\_项**请求本身，则只有当**参数. ProviderId**指向与驱动程序传递到[**的指针相同的设备对象时，才应执行此操作。IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

除非确定系统提供的用户模式组件需要此功能，否则不要实现对**IRP\_MN 的支持\_更改\_单一\_项**。

在处理请求之前，驱动程序必须确定**数据路径**是否指向驱动程序支持的 GUID。 如果未找到，则驱动程序必须失败 IRP 并返回状态\_WMI\_GUID\_不\_。

如果驱动程序支持数据块，则必须检查输入[**WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)结构，这些**参数.** 项结构对实例名称进行指向，如下所示：

-   如果 WNODE\_标记\_静态\_实例在**WnodeHeader**中设置\_名称，则驱动程序使用**InstanceIndex**作为该块的静态实例名称列表中的索引。 WMI 从驱动程序注册块时提供的注册数据中获取索引。

-   如果 WNODE\_标记\_静态\_\_实例在 WnodeHeader 中为空 **，** 则驱动程序将使用**OffsetInstanceName**的偏移量在输入 WNODE 中查找实例名称字符串[ **\_SINGLE\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)结构。 **OffsetInstanceName**是以字节为单位表示的偏移量（以字节为单位）实例名称字符串的 USHORT 大小长度（不是个字符）。 此长度包括 NULL 结束符（如果存在），后跟 Unicode 中的实例名称字符串。

驱动程序负责验证所有输入值。 具体而言，如果驱动程序处理 IRP 请求本身，则必须执行以下操作：

-   对于静态名称，验证 WNODE\_单个\_项结构的**InstanceIndex**成员是否在数据块的驱动程序支持的实例索引范围内。

-   对于动态名称，请验证实例名称字符串是否标识了驱动程序支持的数据块实例。

-   验证 WNODE 的**ItemId**成员[ **\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)结构是否位于数据块的驱动程序支持的项标识符范围内。

-   验证**WNODE\_单个\_项**结构的**DataBlockOffset**和**SizeDataItem**成员是否描述了有效大小的数据块，以及缓冲区的内容是否对数据项有效。

-   验证指定的数据项是否为驱动程序允许调用方启动的修改。 换句话说，驱动程序不应允许修改您打算为只读的数据项。

不要假设线程上下文是启动用户模式应用程序的上下文，较高级别的驱动程序可能已更改了该上下文。

如果驱动程序找不到指定的实例，则它必须失败 IRP 并返回状态\_WMI\_实例\_但找不到\_。 对于具有动态实例名称的实例，此状态指示该驱动程序不支持该实例。 这样，WMI 就可以继续查询其他数据访问接口，如果另一个提供程序找到该实例，但由于其他原因无法处理该请求，则会向数据使用者返回相应的错误。

如果驱动程序找到该实例并可以处理该请求，则会将该实例中的数据项设置为[**WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)中的值。 如果数据项为只读，则驱动程序会使项保持不变，使 IRP 失败，并\_WMI\_只读取\_的状态。

如果实例有效但驱动程序无法处理请求，则它可能会返回任何适当的错误状态。

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


[*DpWmiSetDataItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_单个\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)

 

 




