---
title: WMI WNODE_XXX 结构
description: WMI WNODE_XXX 结构
ms.assetid: 9d059b9a-c129-42ba-8db6-53480003f56e
keywords:
- WMI WDK 内核，请求
- 请求 WDK WMI
- Irp WDK WMI
- WNODE_XXX 结构
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d881f53bbf8b3de4053b514bc858b243e9f14416
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187885"
---
# <a name="wmi-wnode_xxx-structures"></a>WMI WNODE \_ XXX 结构





WMI 使用一组称为 **WNODE \_ * XXX*** 的标准数据结构在用户模式数据使用者和内核模式数据提供程序（如驱动程序）之间传递数据。 如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI 请求，则该驱动程序不需要读取或写入 **WNODE \_ * XXX*** 结构。 否则，驱动程序必须将输入 **WNODE \_ * xxx*** **转换为 WNODE，并/** 或将输出 ** \_ * xxx*** 写入该位置。

下表列出了 WMI Irp 及其相应的 **WNODE \_ * XXX*** 结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WMI IRP</th>
<th>相关 WNODE_XXX 结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](./irp-mn-change-single-instance.md)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](./irp-mn-change-single-item.md)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)"><strong>WNODE_SINGLE_ITEM</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](./irp-mn-execute-method.md)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item" data-raw-source="[&lt;strong&gt;WNODE_METHOD_ITEM&lt;/strong&gt;](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)"><strong>WNODE_METHOD_ITEM</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](./irp-mn-query-all-data.md)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data" data-raw-source="[&lt;strong&gt;WNODE_ALL_DATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)"><strong>WNODE_ALL_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](./irp-mn-query-single-instance.md)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
</tbody>
</table>

 

另外两个 **WNODE \_ * XXX*** 结构（ [**WNODE \_ 事件 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item) 和 [**WNODE \_ 事件 \_ 引用**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)）用于发送已启用事件的通知。 注册事件块的驱动程序，如果已启用事件并发生事件，则通过调用 [**IoWMIWriteEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent) 并传递 **WNODE \_ 事件 \_ * XXX*** 结构，将事件的通知发送到 WMI。 有关发送 WMI 事件的信息，请参阅 [发送 Wmi 事件](sending-wmi-events.md)。

每个 **WNODE \_ * XXX*** 结构包含以下各项：

- 一个嵌入的 [**WNODE \_ 标头**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header) 结构，其中包含所有 **WNODE \_ **（包括缓冲区大小、表示数据块的 GUID）的通用信息，以及指示 **WNODE \_ * XXX*** 结构的类型的标志，无论它使用的是静态还是动态实例名称，以及块的其他特征。

- 特定 **WNODE \_ * XXX*** 结构的固定成员，例如实例名称和数据的偏移量。

IRP 缓冲区中的 **WNODE \_ * XXX*** 结构 (**参数。**) 通常后跟与请求相关的变量数据，如动态实例名称、静态实例名称字符串、方法的输入或从方法的输出或数据块的一个或多个实例的数据。 因此，缓冲区的大小必须超出**sizeof (WNODE \_ *XXX*) **所涉及的变量数据量。

请注意，WMI 不会对驱动程序提供的变量数据执行类型检查。 驱动程序必须将输出数据的输出数据对齐到输出缓冲区中的相应边界，以便数据使用者可以正确地分析数据。 具体而言，每个实例必须在8字节边界上启动，并且每个实例都必须根据驱动程序先前注册的数据块架构在自然边界上对齐。 动态实例名称可以在2字节边界对齐。

下图显示了 IRP 缓冲区的一个框图，其中包含 [**WNODE \_ 单 \_ 实例**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance) 结构，驱动程序可能会返回该结构，以响应 [**IRP \_ MN \_ 查询 \_ 单 \_ 实例**](./irp-mn-query-single-instance.md) 请求。

![说明包含 wnode \- 单一实例的 irp 缓冲区的 \- 示意图](images/wnode-single-instance.png)

从上图的顶部开始：

-   [**WNODE \_ 单 \_ 实例**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)开头的[**WNODE \_ 标头**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)结构包含在**WnodeHeader**成员中。 WMI 将在发送请求之前填写 **WNODE \_ 标头** 的所有成员。 在 **WNODE \_ 标头**中：

    -   **WnodeHeader** 指示 **WNODE \_ 单个 \_ 实例**的大小，包括位于结构的固定成员之后的数据。  (**WnodeHeader** 的值通常小于，这表示 wmi 为接收来自驱动程序的 **输出而分配**的缓冲区大小 ) 
    -   **WnodeHeader** 包含标识数据块的 guid。
    -   在此示例中， **WnodeHeader** 表示此结构是 **WNODE \_ 单一 \_ 实例** ，数据块使用静态实例名称。
-   由于数据块使用静态实例名称，因此 WMI 将 **InstanceIndex** 设置为在注册块时由驱动程序传递的静态实例名称列表中的实例的索引。 不使用**OffsetInstanceNames** 。

-   WMI 设置 **DataBlockOffset** ，以指示从缓冲区开头到实例数据的第一个字节的偏移量。  (驱动程序不能再次更改此值) 因为数据块使用静态实例名称，所以此偏移指示与 **VariableData**相同的位置。 如果数据块使用了动态实例名称，实例名称将从 **VariableData** 开始， **DataBlockOffset** 将在缓冲区中指定一个更大的偏移量。

-   驱动程序将 **SizeDataBlock** 设置为要返回的实例数据的字节数。

-   在实例名称数据后的 **VariableData** (（如果存在) ），驱动程序会在输出缓冲区中写入所请求实例的实例数据。

驱动程序以与**WNODE \_ 单一 \_ 实例**相同的方式读取和写入[**WNODE \_ 方法 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)和[**WNODE \_ 单一 \_ 项**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)结构。 这些结构彼此类似，其中每个都具有固定成员 **OffsetInstanceName**、 **InstanceIndex**、 **DataBlockOffset**、 **SizeDataBlock** (或者，对于 **WNODE \_ 单个 \_ 项**， **SizeDataItem**) 和 **VariableData**。 **WNODE \_方法 \_ 项**包含**MethodId** ， **WNODE \_ 一 \_ 项**包含**WNODE \_ 单个 \_ 实例**缺少的**ItemId** 。

[**WNODE \_所有 \_ 数据**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data) 都不同于前面的结构，因为它用于传递多个数据块实例，可能包含动态实例名称和可能不同的大小。

下图显示了 IRP 缓冲区的一个框图，其中包含一个 WNODE 驱动程序返回的 ** \_ 所有 \_ 数据** ，以响应 [**IRP \_ MN \_ 查询 \_ 所有 \_ 数据**](./irp-mn-query-all-data.md) 请求。

![说明包含 wnode \- 所有数据的 irp 缓冲区的关系图 \-](images/wnode-all-data.png)

从上图的顶部开始：

- 如上图所述，WNODE 开头的[**WNODE \_ 标头**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)结构包含在**WnodeHeader**成员[**中 \_ \_ **](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data) 。 **WnodeHeader** 和 **WnodeHeader** 分别指示 **WNODE \_ 所有 \_ 数据** 的大小和数据块的 Guid。

  在此示例中，WMI 设置 **WnodeHeader** 以指示此结构是 **WNODE \_ 所有 \_ 数据** ，并且数据块已注册到动态实例名称 (也就是说，WMI 清除 WNODE \_ 标记 \_ 静态 \_ 实例 \_ 名称，WNODE \_ 标记 \_ PDO \_ 实例 \_ 名称) 。 在输出时，驱动程序将设置 WNODE \_ 标志 \_ 固定 \_ 实例 \_ 大小，以指示所有实例的大小都相同。

- WMI 设置 **DataBlockOffset** ，以指示从缓冲区开头到实例数据的第一个字节的偏移量。  (驱动程序不得将此值更改) 。 在此示例中，实例数据遵循 **OffsetInstanceNameOffsets**处的实例名称。

- 驱动程序设置 **InstanceCount** 以指示要返回的实例数。

- 使用动态实例名称的数据块的**WNODE \_ * XXX*** 始终包含实例名称字符串。 由于本示例使用动态实例名称，因此 **OffsetInstanceNameOffsets** 指示从缓冲区开头到缓冲区中动态实例名称的偏移数组的偏移量。

- **FixedInstanceSize** 指示驱动程序返回的每个实例中数据的字节数。 如果此数据块的实例大小变化，则驱动程序将清除 WNODE \_ \_ \_ \_ 在 **WnodeHeader** 中标记固定实例大小，并将 **OffsetInstanceDataAndLength** 设置为 **OffsetInstanceDataAndLength** 结构的数组，每个指定一个实例的数据偏移量，而不是设置 **FixedInstanceSize**。

有关 **WNODE \_ * XXX*** 结构的详细信息，请参阅 [系统结构](/windows-hardware/drivers/ddi/index)。

 

