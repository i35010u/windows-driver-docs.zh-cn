---
title: IRP_MN_EXECUTE_METHOD
description: 支持数据块中的方法的所有驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: cc42340e-4a7c-475c-b44d-2127e8a0d7dc
keywords:
- IRP_MN_EXECUTE_METHOD 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 16258bc05ecd45e5292c40c2c4d4ce2cfcff5057
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828058"
---
# <a name="irp_mn_execute_method"></a>IRP\_MN\_EXECUTE\_方法


支持数据块中的方法的所有驱动程序都必须处理此 IRP。 驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理**IRP\_MN\_执行\_方法**请求，则 WMI 反过来会调用该驱动程序的[*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)发送时间
---------

WMI 发送此 IRP 以执行与数据块关联的方法。

WMI 在任意线程上下文中以 IRQL = 被动\_级别发送此 IRP。

在发送**irp\_MN\_EXECUTE\_方法**之前，WMI 会将[**irp\_MN\_QUERY\_单一\_实例**](irp-mn-query-single-instance.md)发送。 如果驱动程序支持**irp\_MN\_执行\_方法**，则它必须具有**irp\_MN\_查询\_** 正在执行其方法的同一数据块的单个\_实例处理程序。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId**指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径**指向标识与要执行的方法关联的数据块的 GUID。

WNODE**指示在** **参数. buffer**的非分页缓冲区的大小。 &gt;必须 = **sizeof**（ **\_方法\_项**）加上任何输出数据的大小，付款方式.

WNODE**将指向** [ **\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)结构，在此结构中， **MethodID**指示要执行的方法的标识符， **DataBlockOffset**指示开始时的偏移量（以字节为单位）到输入数据的第一个字节的结构（如果有）。 **&gt;SizeDataBlock**指示输入**WNODE\_方法\_项**（包括输入数据）的大小（以字节为单位），如果没有输入，则指示零。

## <a name="output-parameters"></a>输出参数


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，wmi 将使用驱动程序的[*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)例程返回的数据来填充[**WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)。

否则，驱动程序会在**WNODE\_方法\_项**结构中填充**参数。**

-   用输出**WNODE\_\_方法**的大小更新**WnodeHeader** ，包括任何输出数据。

-   用输出数据的大小更新**SizeDataBlock** ，如果没有输出数据，则更新零。

-   检查 WNODE 以确定缓冲区是否足够大 **，以便接收**包含任何输出数据的输出 **\_方法\_项**。 如果缓冲区不够大，驱动程序将在 WNODE 中填充所需的大小， [ **\_也不\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)由**PARAMETERS**指向的小型结构。 如果缓冲区小于**sizeof**（**WNODE\_太小\_** ），则该驱动程序将无法 IRP，并\_缓冲区返回状态\_\_太小。

-   写入从**DataBlockOffset**开始的输入数据的输出数据（如果有）。 驱动程序不得更改**DataBlockOffset**的输入值。

## <a name="io-status-block"></a>I/O 状态块


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp&gt;IoStatus**和**irp-&gt;IoStatus** 。

否则，驱动程序会将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS 或适当的错误状态，如下所示：

状态\_缓冲区\_太小\_

找不到\_WMI\_GUID\_的状态\_

找不到\_WMI\_实例的状态\_\_

\_\_WMI ITEMID\_找不到\_

成功时，驱动程序将**Irp&gt;IoStatus**设置为写入**缓冲区中的字节数。**

<a name="operation"></a>操作
---------

驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的[*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)例程，或返回状态\_无效\_设备\_请求（如果驱动程序未定义例程）。

如果驱动程序处理**IRP\_MN\_执行\_方法**请求本身，则只有当 IoWMIRegistrationControl 指向的设备对象与驱动程序传递到[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的指针**相同时，** 才必须这样做。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

驱动程序负责验证所有输入值。 具体而言，如果驱动程序处理 IRP 请求本身，则必须执行以下操作：

-   对于静态名称，验证[**WNODE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)的**INSTANCEINDEX**成员\_项结构是否位于数据块的驱动程序支持的实例索引范围内。

-   对于动态名称，请验证实例名称字符串是否标识了驱动程序支持的数据块实例。

-   验证[**WNODE\_方法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)的**METHODID**成员\_项结构是否在数据块的驱动程序支持的方法标识符范围内，以及是否允许调用方执行此方法。

-   验证[**WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)结构的**DataBlockOffset**和**SizeDataBlock**成员描述一个足以包含指定方法的参数的缓冲区，以及参数是否有效。用于方法。

-   验证 WNODE**指定一个**缓冲区，该缓冲区足以在使用输出数据更新后接收\_项结构的 " **"\_方法**。

不要假设线程上下文是启动用户模式应用程序的上下文，较高级别的驱动程序可能已更改了该上下文。

在处理请求之前，驱动程序必须确定**数据路径**是否指向驱动程序支持的 GUID。 否则，驱动程序必须失败 IRP 并返回状态\_WMI\_GUID\_找不到\_。

如果驱动程序支持数据块，它将检查输入的[**WNODE\_方法\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)实例名称的**参数。**

-   如果 WNODE\_标记\_静态\_实例在**WnodeHeader**中设置\_名称，则驱动程序使用**InstanceIndex**作为该块的静态实例名称列表中的索引。 WMI 通过注册块时驱动程序提供的注册数据获取索引。

-   如果 WNODE\_标记\_静态\_\_实例在 WnodeHeader 中为空 **，** 则驱动程序将使用**OffsetInstanceName**的偏移量在输入**WNODE\_方法中查找实例名称字符串\_ITEM**。 **OffsetInstanceName**是从结构开始到 USHORT 的偏移量（以字节为单位），它是实例名称字符串的长度（以字节为单位），包括终止 null （如果存在），后跟 Unicode 中的实例名称字符串。

如果驱动程序找不到指定的实例，则它必须失败 IRP 并返回状态\_WMI\_实例\_但找不到\_。 对于具有动态实例名称的实例，此状态指示该驱动程序不支持该实例。 这样，WMI 就可以继续查询其他数据访问接口，如果另一个提供程序找到该实例，但由于其他原因无法处理该请求，则会向数据使用者返回相应的错误。

然后，该驱动程序将检查输入\_WNODE 中的方法 ID **\_项**，以确定它是否是该数据块的有效方法。 否则，驱动程序将无法通过 IRP 并返回状态\_WMI\_ITEMID\_找不到\_。

如果该方法生成输出，则驱动程序应在执行任何可能具有副作用或不应执行两次操作的操作之前，检查参数中的输出缓冲区的大小 **。** 例如，如果方法返回一组计数器的值，然后重置计数器，则驱动程序应检查缓冲区大小（如果缓冲区太小，则会在缓冲区过小时失败），然后重置计数器。 这确保了 WMI 可以使用更大的缓冲区安全地重新发送请求。

如果实例和方法 ID 有效并且缓冲区大小充足，则驱动程序将执行方法。 如果 input **WNODE\_\_方法**中的**SizeDataBlock**为非零，则驱动程序将使用从**DataBlockOffset**开始的数据作为该方法的输入。

如果该方法生成输出，则驱动程序将输出数据写入缓冲区中开始的**DataBlockOffset** ，并将**WNODE\_方法\_项**中的**SizeDataBlock**设置为输出数据的字节数。 如果该方法没有输出数据，则驱动程序将**SizeDataBlock**设置为零。 驱动程序不得更改**DataBlockOffset**的输入值。

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


[*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_方法\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)

 

 




