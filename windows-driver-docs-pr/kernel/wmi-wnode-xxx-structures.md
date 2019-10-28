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
ms.openlocfilehash: 813e2d8e4a8a25087d57885d0fbd81a8480a0be8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838302"
---
# <a name="wmi-wnode_xxx-structures"></a>WMI WNODE\_XXX 结构





WMI 使用一组称为**WNODE\_* XXX*** 的标准数据结构在用户模式数据使用者和内核模式数据提供程序（如驱动程序）之间传递数据。 如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI 请求，则该驱动程序不需要读取或写入**WNODE\_* XXX*** 结构。 否则，驱动程序必须将输入**WNODE\_* xxx*****转换为 WNODE，并/** 或将输出 **\_** 写入到该位置。

下表列出了 WMI Irp 及其相应的**WNODE\_* XXX*** 结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WMI IRP</th>
<th>相关的 WNODE_XXX 结构</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)"><strong>WNODE_SINGLE_ITEM</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item" data-raw-source="[&lt;strong&gt;WNODE_METHOD_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)"><strong>WNODE_METHOD_ITEM</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data" data-raw-source="[&lt;strong&gt;WNODE_ALL_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)"><strong>WNODE_ALL_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
</tbody>
</table>

 

另外两个**WNODE\_* XXX*** 结构、 [**WNODE\_事件\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item)和[**WNODE\_事件\_引用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)）用于发送已启用事件的通知。 注册事件块的驱动程序，如果已启用事件并发生事件，则通过调用[**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)并传递**WNODE\_事件\_* XXX*** 结构来向 WMI 发送事件通知。 有关发送 WMI 事件的信息，请参阅[发送 Wmi 事件](sending-wmi-events.md)。

每个**WNODE\_* XXX*** 结构包含以下各项：

- 嵌入的[**WNODE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)结构，其中包含所有**WNODE\_* xxx*** 所共有的信息，包括缓冲区大小、表示数据块的 GUID，以及指示 WNODE 类型的标志 **\_** * 结构，它是使用静态实例名称还是动态实例名称，以及块的其他特征。

- 特定**WNODE\_* XXX*** 结构的固定成员，例如实例名称和数据的偏移量。

IRP**缓冲区（** WNODE）中的 **\_* XXX*** 结构通常后跟与请求相关的变量数据，如动态实例名称、静态实例名称字符串、方法的输入或从方法的输出或数据对于一个或多个数据块实例。 因此，缓冲区的大小必须按所涉及的变量数据量超过**sizeof （WNODE\_*XXX*）** 。

请注意，WMI 不会对驱动程序提供的变量数据执行类型检查。 驱动程序必须将输出数据的输出数据对齐到输出缓冲区中的相应边界，以便数据使用者可以正确地分析数据。 具体而言，每个实例必须在8字节边界上启动，并且每个实例都必须根据驱动程序先前注册的数据块架构在自然边界上对齐。 动态实例名称可以在2字节边界对齐。

下图显示了一个 IRP 缓冲区框图，其中包含一个[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构，驱动程序可能会返回该结构，以响应[**IRP\_MN\_查询\_单\_实例**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)需要.

![阐释包含 wnode\-单个\-实例的 irp 缓冲区的关系图](images/wnode-single-instance.png)

从上图的顶部开始：

-   [**WNODE\_单\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)开头的[**WNODE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)结构包含在**WnodeHeader**成员中。 WMI 将在发送请求之前填写**WNODE\_标头**的所有成员。 在**WNODE\_标头**：

    -   **WnodeHeader**指示**WNODE\_单个\_实例**的大小，包括位于结构的固定成员之后的数据。 （ **WnodeHeader**的值通常小于，这表示 wmi 为接收来自驱动程序的输出而分配的缓冲区的**大小。）**
    -   **WnodeHeader**包含标识数据块的 guid。
    -   在此示例中， **WnodeHeader**表示此结构是一个**WNODE\_单个\_实例**，数据块使用静态实例名称。
-   由于数据块使用静态实例名称，因此 WMI 将**InstanceIndex**设置为在注册块时由驱动程序传递的静态实例名称列表中的实例的索引。 不使用**OffsetInstanceNames** 。

-   WMI 设置**DataBlockOffset** ，以指示从缓冲区开头到实例数据的第一个字节的偏移量。 （驱动程序不得更改此值）由于数据块使用静态实例名称，因此此偏移指示与**VariableData**相同的位置。 如果数据块使用了动态实例名称，实例名称将从**VariableData**开始， **DataBlockOffset**将在缓冲区中指定一个更大的偏移量。

-   驱动程序将**SizeDataBlock**设置为要返回的实例数据的字节数。

-   在**VariableData** （实例名称数据后，如果存在），驱动程序将在输出缓冲区中写入所请求实例的实例数据。

驱动程序读取并写入[**WNODE\_方法\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)和[**WNODE\_单一\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)结构，其方式与**WNODE\_单个\_实例**的方式几乎相同。 这些结构彼此类似，其中每个都具有固定成员**OffsetInstanceName**、 **InstanceIndex**、 **DataBlockOffset**、 **SIZEDATABLOCK** （对于**WNODE\_单个\_项**， **SizeDataItem**）和**VariableData**。 **WNODE\_方法\_项**包括**MethodId**和**WNODE\_单一\_项**包含一个 **\_\_单个实例**的**ItemId** 。

[**WNODE\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)与前面的结构不同，因为它用于传递多个数据块实例，可能包含动态实例名称和可能不同的大小。

下图显示了 IRP 缓冲区的一个框图，其中包含一个 WNODE\_驱动程序返回的**所有\_数据**，以响应[**IRP\_MN\_查询\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)请求。

![阐释包含 wnode\-所有\-数据的 irp 缓冲区的关系图](images/wnode-all-data.png)

从上图的顶部开始：

- 如上图中所述，WNODE 开头的[**WNODE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)结构[ **\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)都包含在**WnodeHeader**成员中。 **WnodeHeader**和**WnodeHeader**分别指示**WNODE\_所有\_数据**的大小和数据块的 Guid。

  在此示例中，WMI 设置**WnodeHeader** ，以指示此结构是**所有\_数据的 WNODE\_** 并且数据块已注册到动态实例名称（也就是说，WMI 清除 WNODE\_标志\_静态\_实例\_名称和 WNODE\_标志\_PDO\_实例\_名称）。 在输出时，驱动程序将 WNODE\_标记设置\_固定\_\_实例的大小，以指示所有实例大小都相同。

- WMI 设置**DataBlockOffset** ，以指示从缓冲区开头到实例数据的第一个字节的偏移量。 （驱动程序不得更改此值）。 在此示例中，实例数据遵循**OffsetInstanceNameOffsets**处的实例名称。

- 驱动程序设置**InstanceCount**以指示要返回的实例数。

- 使用动态实例名称的数据块的**WNODE\_* XXX*** 始终包含实例名称字符串。 由于本示例使用动态实例名称，因此**OffsetInstanceNameOffsets**指示从缓冲区开头到缓冲区中动态实例名称的偏移数组的偏移量。

- **FixedInstanceSize**指示驱动程序返回的每个实例中数据的字节数。 如果此数据块的实例大小变化，则驱动程序将清除 WNODE\_标记\_固定\_ **\_实例，并将**OffsetInstanceDataAndLength 设置为数组大小，并将设置为数组**OFFSETINSTANCEDATAANDLENGTH**结构，每个结构指定一个实例的数据偏移量以及该实例中的字节数，而不是设置**FixedInstanceSize**。

有关**WNODE\_* XXX*** 结构的详细信息，请参阅[系统结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

 

 




