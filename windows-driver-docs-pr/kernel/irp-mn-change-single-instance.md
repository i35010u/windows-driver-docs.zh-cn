---
title: IRP_MN_CHANGE_SINGLE_INSTANCE
description: 支持 WMI 的所有驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 180d40a4-b300-4801-b9da-9239500ca15f
keywords:
- IRP_MN_CHANGE_SINGLE_INSTANCE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: f128b6d1a496b3e9394844c0f0e8e859215af020
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382246"
---
# <a name="irpmnchangesingleinstance"></a>IRP\_MN\_更改\_单个\_实例


支持 WMI 的所有驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)处理**IRP\_MN\_更改\_单一\_实例**请求 WMI 又会调用该驱动程序[ *DpWmiSetDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_datablock_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将发送此 IRP，若要更改的数据块的单个实例中的所有数据项。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 在驱动程序的 I/O 堆栈位置中找到此指针。

**Parameters.WMI.DataPath**指向标识数据块的 GUID 与要更改的实例相关联。

**Parameters.WMI.BufferSize**指示在非分页缓冲区的大小**Parameters.WMI.Buffer**。

**Parameters.WMI.Buffer**指向[ **WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)结构，它标识的实例并指定新的数据值。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_WMI\_实例\_不\_找到

状态\_WMI\_GUID\_不\_找到

状态\_WMI\_读取\_仅

状态\_WMI\_设置\_失败

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**为零。

<a name="operation"></a>操作
---------

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，例程调用的驱动程序[ *DpWmiSetDataBlock* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_datablock_callback)例程，或返回状态\_WMI\_读取\_仅当驱动程序不会定义该例程。

如果驱动程序处理**IRP\_MN\_更改\_单个\_实例**请求本身，它是仅当设备对象指针位于**Parameters.WMI.ProviderId**匹配驱动程序对其调用中传递的指针[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

如果该驱动程序处理请求，则它必须首先检查在 GUID **Parameters.WMI.DataPath**以确定它是否标识驱动程序支持的数据块。 如果不是，该驱动程序必须失败 IRP，并返回状态\_WMI\_GUID\_不\_找到。

如果该驱动程序支持的数据块，则必须检查接收[ **WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)结构在**Parameters.WMI.Buffer**实例名称，按如下所示：

-   如果 WNODE\_标志\_静态\_实例\_中设置的名称**WnodeHeader.Flags**，则驱动程序使用**InstanceIndex**作为中的索引为该块的静态实例名称的驱动程序的列表。 WMI 从注册块时，驱动程序提供的注册数据中获取索引。

-   如果 WNODE\_标志\_静态\_实例\_名称是明确**WnodeHeader.Flags，** 驱动程序使用的偏移量**OffsetInstanceName**到输入中找到的实例名称字符串[ **WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)。 **OffsetInstanceName**包括终止 null （如果存在） 中从结构开始到 USHORT 大小以字节为单位 （不是字符），实例名称字符串的长度的字节的偏移量后跟以 unicode 格式的实例名称字符串。

该驱动程序负责验证所有输入的值。 具体而言，如果处理 IRP 请求本身，则该驱动程序，就必须执行以下操作：

-   对于静态名称，请验证**InstanceIndex**的成员[ **WNODE\_单一\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)结构位于范围内支持的数据块的驱动程序的实例索引。

-   有关动态名称，验证实例名称字符串标识驱动程序支持的数据块实例。

-   确认**DataBlockOffset**并**SizeDataBlock**的成员**WNODE\_单一\_实例**结构描述有效大小数据块，包括所有填充的数据之间存在项，且适用于数据块的缓冲区的内容。

-   确保指定的数据块是为其驱动程序允许调用方启动的修改。 换而言之，驱动程序不应允许对数据块的计划是只读的修改。

不要假定线程上下文是起始用户模式应用程序 — 更高级别的驱动程序可能已更改它。

如果该驱动程序找不到指定的实例，它必须失败 IRP，并返回状态\_WMI\_实例\_不\_找到。 如果该实例具有一个动态实例名称，此状态指示驱动程序不支持该实例。 因此，WMI 可以继续查询其他数据提供程序，并返回相应的错误数据使用者，如果另一个提供程序的实例，但由于某种原因无法处理该请求。

如果驱动程序查找该实例，并可以处理该请求，它设置为中的值的实例中的可写数据项[ **WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)结构，任何只读项不做任何更改。 如果整个数据块是只读的该驱动程序应失败 IRP，并且返回状态\_WMI\_读取\_仅。

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


[*DpWmiSetDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_set_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




