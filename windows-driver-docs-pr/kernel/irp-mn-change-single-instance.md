---
title: IRP_MN_CHANGE_SINGLE_INSTANCE
description: 支持 WMI 的所有驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 180d40a4-b300-4801-b9da-9239500ca15f
keywords:
- IRP_MN_CHANGE_SINGLE_INSTANCE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 165ece0d12abd69f431bf154646435362021b654
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922567"
---
# <a name="irp_mn_change_single_instance"></a>IRP\_MN\_更改\_单一\_实例


支持 WMI 的所有驱动程序都必须处理此 IRP。 驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理**IRP\_MN\_CHANGE\_单一\_实例**请求，则 WMI 反过来会调用该驱动程序的[*DpWmiSetDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)例程。

<a name="major-code"></a>主要代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)

<a name="when-sent"></a>发送时间
---------

WMI 发送此 IRP 以更改数据块的单个实例中的所有数据项。

WMI 在任意线程上下文中以 IRQL\_= 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId**指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径**指向标识与要更改的实例关联的数据块的 GUID。

**参数. BufferSize**指示非分页缓冲区在**参数. buffer**的大小。

[**WNODE\_\_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)指向标识实例的单个实例结构，并指定新的数据**值。**

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/o 状态块


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp-&gt;IoStatus**和**irp-&gt;IoStatus。**

否则，驱动程序会将**Irp&gt;-IOSTATUS**设置为状态\_成功，或设置为适当的错误状态，如下所示：

找\_不\_\_到\_WMI 实例的状态

找\_不\_\_到\_WMI GUID 状态

状态\_WMI\_只读\_

状态\_WMI\_设置\_失败

成功时，驱动程序将**Irp-&gt;IoStatus**设置为零。

<a name="operation"></a>操作
---------

如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的[*DpWmiSetDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)例程，\_或\_仅\_当驱动程序未定义例程时返回状态 WMI READ。

如果驱动程序处理**\_IRP MN\_更改\_单一\_实例**请求本身，则仅当**参数. ProviderId**中的设备对象指针与驱动程序在其对[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的调用中传递的指针匹配时，才会执行此操作。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

如果驱动程序处理请求，则必须首先检查**数据路径**中的 GUID，以确定它是否标识驱动程序所支持的数据块。 如果不是，则驱动程序必须失败 IRP 并返回\_状态\_WMI\_GUID\_找不到。

如果驱动程序支持数据块，则它必须在**参数. Buffer**中检查收到的[**\_WNODE 单\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构，以了解实例名称，如下所示：

-   如果在\_WnodeHeader\_中\_设置\_了 WNODE 标志静态**WnodeHeader.Flags**实例名称，驱动程序将使用**InstanceIndex**作为该块的静态实例名称列表的索引。 WMI 从驱动程序注册块时提供的注册数据中获取索引。

-   如果 WNODE\_标记\_静态\_实例\_名称在 WnodeHeader 中清晰 **，** 驱动程序将使用**OffsetInstanceName**处的偏移量在输入[**\_WNODE 单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)中查找实例名称字符串。 **OffsetInstanceName**是以字节为单位表示的偏移量（以字节为单位）表示的实例名称字符串的 USHORT 大小长度的偏移量（以字节为单位），包括终止 null （如果存在），后跟 Unicode 中的实例名称字符串。

驱动程序负责验证所有输入值。 具体而言，如果驱动程序处理 IRP 请求本身，则必须执行以下操作：

-   对于静态名称，验证[**WNODE\_\_单实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构的**InstanceIndex**成员是否在数据块的驱动程序支持的实例索引范围内。

-   对于动态名称，请验证实例名称字符串是否标识了驱动程序支持的数据块实例。

-   验证**WNODE\_单一\_实例**结构的**DataBlockOffset**和**SizeDataBlock**成员是否描述了有效大小的数据块，包括数据项之间存在的任何填充，以及缓冲区的内容对于数据块是否有效。

-   验证指定的数据块是否为驱动程序允许调用方启动的修改。 换句话说，驱动程序不应允许修改您打算为只读的数据块。

不要假设线程上下文是启动用户模式应用程序的上下文，较高级别的驱动程序可能已更改了该上下文。

如果驱动程序找不到指定的实例，则该驱动程序必须失败 IRP\_并\_返回\_状态\_WMI 实例找不到。 如果该实例具有动态实例名称，则此状态指示该驱动程序不支持该实例。 这样，WMI 就可以继续查询其他数据访问接口，如果另一个提供程序找到该实例，但由于其他原因无法处理该请求，则会向数据使用者返回相应的错误。

如果驱动程序找到该实例并可以处理该请求，则会将该实例中的可写数据项设置为[**\_WNODE 单\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构中的值，使所有只读项保持不变。 如果整个数据块为只读，则驱动程序应失败 IRP 并返回状态\_WMI\_只读。\_

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DpWmiSetDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_单\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




