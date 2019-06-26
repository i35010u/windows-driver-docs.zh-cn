---
title: IRP_MN_EXECUTE_METHOD
description: 支持的数据块中的方法的所有驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: cc42340e-4a7c-475c-b44d-2127e8a0d7dc
keywords:
- IRP_MN_EXECUTE_METHOD 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: bbc089c4d3fc154e223a3981a5d094a7454a8090
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353358"
---
# <a name="irpmnexecutemethod"></a>IRP\_MN\_EXECUTE\_METHOD


支持的数据块中的方法的所有驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)处理**IRP\_MN\_EXECUTE\_方法**请求时，WMI 反过来调用驱动程序的[ *DpWmiExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将发送此 IRP 来执行与数据块关联的方法。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

WMI 将发送[ **IRP\_MN\_查询\_单一\_实例**](irp-mn-query-single-instance.md)在发送前**IRP\_MN\_EXECUTE\_方法**。 如果驱动程序支持**IRP\_MN\_EXECUTE\_方法**必须拥有**IRP\_MN\_查询\_单一\_实例**正在执行的方法在同一个数据块的处理程序。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**指向标识数据块的 GUID 与要执行的方法相关联。

**Parameters.WMI.BufferSize**指示在非分页缓冲区的大小**Parameters.WMI.Buffer**它必须是&gt; =  **sizeof**(**WNODE\_方法\_项**) 以及任何大小输出数据的方法。

**Parameters.WMI.Buffer**指向[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)结构在其中**MethodID**指示要执行的方法的标识符和**DataBlockOffset**指示中第一个字节的输入数据，从结构开始的字节偏移量。 **Parameters.WMI.Buffer-&gt;SizeDataBlock**指示以字节为单位输入的大小**WNODE\_方法\_项**包括输入的数据，或如果没有任何输入为零。

## <a name="output-parameters"></a>输出参数


如果该驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 会填写[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)返回的驱动程序的数据[ *DpWmiExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)例程。

否则，该驱动程序会填写**WNODE\_方法\_项**结构的**Parameters.WMI.Buffer**指向，如下所示：

-   更新**WnodeHeader.BufferSize**输出的大小**WNODE\_方法\_项**，包括任何输出数据。

-   更新**SizeDataBlock**输出数据，则为零，如果没有输出数据的大小。

-   检查**Parameters.WMI.Buffersize**若要确定缓冲区是否足够大，以接收输出**WNODE\_方法\_项**包括任何输出数据。 如果缓冲区足够大，驱动程序填充中的所需的大小，以[ **WNODE\_过\_小**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_too_small)指向结构**Parameters.WMI.Buffer**. 如果缓冲区小于**sizeof**(**WNODE\_过\_小**)，该驱动程序将 IRP 失败并返回状态\_缓冲区\_过\_小。

-   如果有，通过输入的数据开始写入输出数据**DataBlockOffset**。 该驱动程序不得更改的输入的值**DataBlockOffset**。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_缓冲区\_过\_小

状态\_WMI\_GUID\_不\_找到

状态\_WMI\_实例\_不\_找到

状态\_WMI\_ITEMID\_不\_找到

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**写入的缓冲区的字节数**Parameters.WMI.Buffer**。

<a name="operation"></a>操作
---------

驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)。

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)，例程调用的驱动程序[ *DpWmiExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)例程，或返回状态\_无效\_设备\_请求如果驱动程序不会定义该例程。

如果驱动程序处理**IRP\_MN\_EXECUTE\_方法**请求本身，它必须执行此操作仅当**Parameters.WMI.ProviderId**指向与相同的设备对象该驱动程序传递到指针[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

该驱动程序负责验证所有输入的值。 具体而言，如果处理 IRP 请求本身，则该驱动程序，就必须执行以下操作：

-   对于静态名称，请验证**InstanceIndex**的成员[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)结构是实例的范围内支持的数据块的驱动程序的索引。

-   有关动态名称，验证实例名称字符串标识驱动程序支持的数据块实例。

-   确认**MethodId**的成员[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)结构是支持的方法标识符的范围内数据块，该驱动程序并允许调用方来执行此方法。

-   确认**DataBlockOffset**并**SizeDataBlock**的成员[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)结构描述的缓冲区足够大不能包含指定的方法的参数和参数都是有效的方法。

-   确认**Parameters.WMI.Buffersize**指定足够大，接收的缓冲区**WNODE\_方法\_项**结构更新与输出后数据。

不要假定线程上下文是起始用户模式应用程序 — 更高级别的驱动程序可能已更改它。

之前处理请求，该驱动程序必须确定是否**Parameters.WMI.DataPath**指向驱动程序支持的 GUID。 如果不是，该驱动程序必须失败 IRP，并返回状态\_WMI\_GUID\_不\_找到。

如果该驱动程序支持的数据块，它会检查输入[ **WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)在**Parameters.WMI.Buffer**实例名称按如下所示：

-   如果 WNODE\_标志\_静态\_实例\_中设置的名称**WnodeHeader.Flags**，则驱动程序使用**InstanceIndex**作为中的索引为该块的静态实例名称的驱动程序的列表。 WMI 从注册块时驱动程序提供的注册数据中获取索引。

-   如果 WNODE\_标志\_静态\_实例\_名称是明确**WnodeHeader.Flags，** 驱动程序使用的偏移量**OffsetInstanceName**到输入中找到的实例名称字符串**WNODE\_方法\_项**。 **OffsetInstanceName**是从结构开始到 USHORT 这是实例名称字符串长度以字节为单位 （不是字符），如果存在后, 跟实例名称字符串中包括终止 null 字节中的偏移量Unicode。

如果该驱动程序找不到指定的实例，它必须失败 IRP，并返回状态\_WMI\_实例\_不\_找到。 对于使用动态实例名称的实例，此状态指示驱动程序不支持该实例。 因此，WMI 可以继续查询其他数据提供程序，并返回相应的错误数据使用者，如果另一个提供程序的实例，但由于某种原因无法处理该请求。

该驱动程序会检查输入中的方法 ID **WNODE\_方法\_项**以确定它是否是有效的方法为该数据块。 如果不是，该驱动程序失败 IRP，并返回状态\_WMI\_ITEMID\_不\_找到。

如果此方法将生成输出，该驱动程序应检查中的输出缓冲区的大小**Parameters.WMI.BufferSize**之前执行任何操作，可能会产生负面影响或，不应执行两次。 例如，如果方法返回一组计数器的值，然后将计数器重置该驱动程序应检查缓冲区大小 （和失败 IRP，如果缓冲区太小） 之前重置计数器。 这可确保 WMI 可以安全地重新发送具有较大的缓冲区的请求。

如果缓冲区已足够大小的实例和方法 ID 有效，则该驱动程序执行方法。 如果**SizeDataBlock**中输入**WNODE\_方法\_项**为非零值，驱动程序使用的数据开始**DataBlockOffset**作为输入为方法。

如果此方法将生成输出，则该驱动程序将输出数据写入开始的缓冲区**DataBlockOffset** ，并设置**SizeDataBlock**输出中**WNODE\_方法\_项**到输出数据的字节数。 如果该方法没有输出数据，该驱动程序设置**SizeDataBlock**为零。 该驱动程序不得更改的输入的值**DataBlockOffset**。

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


[*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)

 

 




