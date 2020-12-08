---
title: IRP_MN_EXECUTE_METHOD
description: 支持数据块中的方法的所有驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
keywords:
- IRP_MN_EXECUTE_METHOD Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 06bc66e7868ab25c7e151aa1de9d739e75ea7c13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840331"
---
# <a name="irp_mn_execute_method"></a>IRP \_ MN \_ EXECUTE \_ 方法


支持数据块中的方法的所有驱动程序都必须处理此 IRP。 驱动程序可以通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 或处理 IRP 本身来处理 wmi irp，如 [处理 WMI 请求](./handling-wmi-requests.md)中所述。

如果驱动程序调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 来处理 **IRP \_ MN \_ EXECUTE \_ 方法** 请求，则 WMI 反过来会调用该驱动程序的 [*DpWmiExecuteMethod*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback) 例程。

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ 系统 \_ 控件**](irp-mj-system-control.md)

<a name="when-sent"></a>发送时间
---------

WMI 发送此 IRP 以执行与数据块关联的方法。

WMI \_ 在任意线程上下文中以 IRQL = 被动级别发送此 IRP。

WMI 将在发送 **irp \_ MN \_ EXECUTE \_ 方法** 之前发送 [**irp \_ MN \_ 查询 \_ 单一 \_ 实例**](irp-mn-query-single-instance.md)。 如果驱动程序支持 **irp \_ MN \_ EXECUTE \_ 方法** ，则该方法必须为正在执行其方法的同一数据块提供 **IRP \_ MN \_ 查询 \_ 单一 \_ 实例** 处理程序。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId** 指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径** 指向标识与要执行的方法关联的数据块的 GUID。

WNODE **指示在****参数.**) 的非分页缓冲区的大小，该缓冲区必须是 &gt; =  **sizeof** (**\_ 方法 \_ 项** 加上该方法的任何输出数据的大小。

[**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)结构，其中 **MethodID** 指示要执行的方法的标识符，而 **DataBlockOffset** 指示从结构开始到输入数据的第一个字节（如果有）的偏移量（以字节为单位 **）。** **Parameters。 &gt;SizeDataBlock** 指示输入 **WNODE \_ 方法 \_ 项** （包括输入数据）的大小（以字节为单位），如果没有输入，则为零。

## <a name="output-parameters"></a>输出参数


如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，wmi 将使用驱动程序的 [*DpWmiExecuteMethod*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)例程返回的数据填充 [**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)。

否则，驱动程序会在 **WNODE \_ 方法 \_ 项** 结构中填充 **参数。**

-   用输出 **WNODE \_ 方法 \_ 项** 的大小（包括任何输出数据）更新 **WnodeHeader。**

-   用输出数据的大小更新 **SizeDataBlock** ，如果没有输出数据，则更新零。

-   检查 **WNODE** 以确定缓冲区是否足够大，以便接收包含任何输出数据的输出 **\_ 方法 \_ 项** 。 如果缓冲区不够大，则驱动程序将在 [**WNODE 的 \_ 太 \_ 小**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)结构中填充所需的 **大小。** 如果缓冲区小于 **sizeof** (**WNODE \_ 太 \_ 小**) ，则该驱动程序将失败 IRP 并返回状态 \_ 缓冲区 \_ 太 \_ 小。

-   写入从 **DataBlockOffset** 开始的输入数据的输出数据（如果有）。 驱动程序不得更改 **DataBlockOffset** 的输入值。

## <a name="io-status-block"></a>I/o 状态块


如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置 **irp- &gt; IoStatus** 和 **irp- &gt; IoStatus。**

否则，驱动程序会将 **Irp- &gt; IoStatus** 设置为状态 \_ 成功，或设置为适当的错误状态，如下所示：

状态 \_ 缓冲区 \_ 太 \_ 小

\_ \_ \_ 找不到 WMI \_ GUID 状态

\_ \_ \_ 找不到 WMI \_ 实例的状态

状态 \_ WMI \_ ITEMID \_ \_ 找不到

成功时，驱动程序将 **Irp- &gt; IoStatus** 设置为写入 **缓冲区中的字节数。**

<a name="operation"></a>操作
---------

驱动程序可以通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 或处理 IRP 本身来处理 wmi irp，如 [处理 WMI 请求](./handling-wmi-requests.md)中所述。

如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的 [*DpWmiExecuteMethod*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback) 例程，或在 \_ \_ \_ 驱动程序未定义例程时返回状态 "无效设备请求"。

如果驱动程序处理 **IRP \_ MN \_ EXECUTE \_ 方法** 请求本身，则只有在 **参数. ProviderId** 指向与驱动程序传递给 [**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的指针相同的设备对象时，才必须这样做。 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

驱动程序负责验证所有输入值。 具体而言，如果驱动程序处理 IRP 请求本身，则必须执行以下操作：

-   对于静态名称，验证 [**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)结构的 **InstanceIndex** 成员是否在数据块的驱动程序支持的实例索引范围内。

-   对于动态名称，请验证实例名称字符串是否标识了驱动程序支持的数据块实例。

-   验证 [**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)结构的 **MethodId** 成员是否在数据块的驱动程序支持的方法标识符范围内，以及是否允许调用方执行此方法。

-   验证 [**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)结构的 **DataBlockOffset** 和 **SizeDataBlock** 成员是否描述了足以包含指定方法的参数的缓冲区，以及参数对于方法是否有效。

-   验证 WNODE **指定一个** 缓冲区，该缓冲区足以在使用输出数据更新后接收到 **\_ 方法 \_ 项** 结构。

不要假设线程上下文是启动用户模式应用程序的上下文，较高级别的驱动程序可能已更改了该上下文。

在处理请求之前，驱动程序必须确定 **数据路径** 是否指向驱动程序支持的 GUID。 如果不是，则驱动程序必须失败 IRP 并返回 \_ 状态 \_ WMI \_ GUID \_ 找不到。

如果驱动程序支持数据块，它将在 **参数. Buffer** 中检查实例名称的输入 [**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)，如下所示：

-   如果 \_ \_ \_ \_ 在 **WnodeHeader** 中设置了 WNODE 标志静态实例名称，驱动程序将使用 **InstanceIndex** 作为该块的静态实例名称列表的索引。 WMI 通过注册块时驱动程序提供的注册数据获取索引。

-   如果 WNODE \_ 标记 \_ 静态 \_ 实例 \_ 名称在 **WnodeHeader** 中清晰，驱动程序将使用 **OffsetInstanceName** 处的偏移量在 input **WNODE \_ 方法 \_ 项** 中查找实例名称字符串。 **OffsetInstanceName** 是从结构开始到第 USHORT 的偏移量（以字节为单位），这是实例名称字符串的长度（以字节为单位） (不) 个字符，包括终止 null （如果存在），后跟 Unicode 中的实例名称字符串。

如果驱动程序找不到指定的实例，则该驱动程序必须失败 IRP 并返回状态 \_ WMI \_ 实例 \_ 找不到 \_ 。 对于具有动态实例名称的实例，此状态指示该驱动程序不支持该实例。 这样，WMI 就可以继续查询其他数据访问接口，如果另一个提供程序找到该实例，但由于其他原因无法处理该请求，则会向数据使用者返回相应的错误。

然后，该驱动程序将检查输入 **WNODE \_ 方法 \_ 项** 中的方法 ID，以确定它是否是该数据块的有效方法。 否则，驱动程序将无法进行 IRP，并返回状态 \_ WMI \_ ITEMID " \_ 未找到" \_ 。

如果该方法生成输出，则驱动程序应在执行任何可能具有副作用或不应执行两次操作的操作之前，检查参数中的输出缓冲区的大小 **。** 例如，如果方法返回一组计数器的值，然后重置计数器，则驱动程序应检查缓冲区大小 (如果缓冲区太小) ，则在重置计数器之前，会使 IRP 失败。 这确保了 WMI 可以使用更大的缓冲区安全地重新发送请求。

如果实例和方法 ID 有效并且缓冲区大小充足，则驱动程序将执行方法。 如果输入 **WNODE \_ 方法 \_ 项** 中的 **SizeDataBlock** 为非零值，则驱动程序将使用从 **DataBlockOffset** 开始的数据作为方法的输入。

如果该方法生成输出，则驱动程序将输出数据写入缓冲区，该缓冲区从 **DataBlockOffset** 开始，并将 output **WNODE \_ 方法 \_ 项** 中的 **SizeDataBlock** 设置为输出数据的字节数。 如果该方法没有输出数据，则驱动程序将 **SizeDataBlock** 设置为零。 驱动程序不得更改 **DataBlockOffset** 的输入值。

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

## <a name="see-also"></a>请参阅


[*DpWmiExecuteMethod*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)

[**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)

 

