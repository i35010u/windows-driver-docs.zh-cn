---
title: WMI WNODE_XXX 结构
description: WMI WNODE_XXX 结构
ms.assetid: 9d059b9a-c129-42ba-8db6-53480003f56e
keywords:
- WMI WDK 内核请求
- 请求 WDK WMI
- Irp WDK WMI
- WNODE_XXX 结构
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53bb5d6bbc1713329753106b2063ebe526ca9157
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327253"
---
# <a name="wmi-wnodexxx-structures"></a>WMI WNODE\_XXX 结构





WMI 使用一组标准数据结构称为**WNODE\_* XXX*** 例如驱动程序的数据提供程序用户模式数据使用者和内核模式之间传递数据。 如果驱动程序处理 WMI 请求是通过调用[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，该驱动程序不需要读取或写入**WNODE\_* XXX*** 结构。 否则，该驱动程序必须将输入解释**WNODE\_* XXX*** 处**Parameters.WMI.Buffer**和/或写入输出**WNODE\_* XXX*** 到该位置。

下表列出了 WMI Irp 和其对应**WNODE\_* XXX*** 结构。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550831" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550831)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566377" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566377)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550836" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550836)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566378" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566378)"><strong>WNODE_SINGLE_ITEM</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550868" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550868)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566376" data-raw-source="[&lt;strong&gt;WNODE_METHOD_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566376)"><strong>WNODE_METHOD_ITEM</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551650" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551650)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566372" data-raw-source="[&lt;strong&gt;WNODE_ALL_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566372)"><strong>WNODE_ALL_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551718" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551718)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566377" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566377)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
</tbody>
</table>

 

两个附加**WNODE\_* XXX*** 结构[ **WNODE\_事件\_项**](https://msdn.microsoft.com/library/windows/hardware/ff566373)和[ **WNODE\_事件\_引用**](https://msdn.microsoft.com/library/windows/hardware/ff566374)，用于发送通知的已启用的事件。 注册事件块的驱动程序会如果该事件已启用，并且在事件发生，向发送通知事件的 WMI 通过调用[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)并传递**WNODE\_事件\_* XXX*** 结构。 有关发送 WMI 事件的信息，请参阅[发送 WMI 事件](sending-wmi-events.md)。

每个**WNODE\_* XXX*** 结构包括以下：

- 嵌入[ **WNODE\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566375)结构，其中包含信息普遍适用于所有**WNODE\_* XXX*** 包括缓冲区的大小表示数据块，并标记用于指示的类型的 GUID **WNODE\_* XXX*** 结构，无论它使用静态或动态实例名称和块的其他特征。

- 特定的固定的成员**WNODE\_* XXX*** 结构，如实例名称和数据的偏移量。

一个**WNODE\_* XXX*** IRP 缓冲区中的结构 (**Parameters.WMI.Buffer**) 通常跟与相关的请求，如动态实例名称，静态实例名称的变量数据字符串的输入或输出的方法或数据块的一个或多个实例的数据。 因此必须超过缓冲区的大小**sizeof (WNODE\_*XXX*)** 通过变量的数据量涉及。

请注意，WMI 不会执行上一个驱动程序提供的变量数据类型检查。 驱动程序必须保持一致的输出缓冲区中的相应边界上的输出数据，以便数据使用者可以正确分析数据。 具体而言，每个实例必须 8 字节边界上启动，并且其项的每个必须根据以前注册的驱动程序的数据块架构的自然边界上对齐。 可以在 2 字节边界上对齐动态实例名称。

下图显示了一个 IRP 缓冲区，其中包含的框图[ **WNODE\_单个\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff566377)结构的驱动程序可能会返回响应[ **IRP\_MN\_查询\_单一\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff551718)请求。

![说明包含 wnode irp 缓冲区的关系图\-单个\-实例](images/wnode-single-instance.png)

开始在上图中的顶部：

-   [ **WNODE\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566375)结构的开头[ **WNODE\_单一\_实例**](https://msdn.microsoft.com/library/windows/hardware/ff566377)中包含**WnodeHeader**成员。 WMI 中的所有成员将填充**WNODE\_标头**之前发送请求。 在中**WNODE\_标头**:

    -   **WnodeHeader.Buffersize**指示的大小**WNODE\_单个\_实例**，包括遵循固定结构的成员的数据。 (的值**WnodeHeader.Buffersize**是通常小于**Parameters.WMI.Buffersize**，指示 WMI 来接收来自该驱动程序的输出所分配的缓冲区的大小。)
    -   **WnodeHeader.Guid**包含标识的数据块的 GUID。
    -   在此示例中， **WnodeHeader.Flags**指示此结构是**WNODE\_单个\_实例**数据块，使用静态和实例的名称。
-   WMI 数据块使用静态实例名称，因为设置**InstanceIndex**的索引的列表中的静态实例名时注册块传递由驱动程序的实例。 **OffsetInstanceNames**不使用。

-   WMI 集**DataBlockOffset**以指示从缓冲区的开头到实例数据的第一个字节的偏移量。 （该驱动程序必须更改此值）再次数据块使用静态实例名称，因为此偏移量指示与相同的位置**VariableData**。 如果使用动态实例名称的数据块，实例名称将开始在**VariableData**并**DataBlockOffset**会指定更大的偏移量到缓冲区。

-   驱动程序集**SizeDataBlock**到返回的实例数据的字节数。

-   在**VariableData** （实例名称数据之后，如果存在），该驱动程序将请求的实例的实例数据写入输出缓冲区中。

驱动程序读取和写入[ **WNODE\_方法\_项**](https://msdn.microsoft.com/library/windows/hardware/ff566376)并[ **WNODE\_单一\_项**](https://msdn.microsoft.com/library/windows/hardware/ff566378)方法与大致相同的结构**WNODE\_单一\_实例**。 这些结构类似于彼此，每个都有固定的成员**OffsetInstanceName**， **InstanceIndex**， **DataBlockOffset**， **SizeDataBlock** (或的情况下**WNODE\_单个\_项**， **SizeDataItem**) 和**VariableData**. **WNODE\_方法\_项**包括**MethodId**并**WNODE\_单一\_项**包括**ItemId**这**WNODE\_单个\_实例**缺少。

[**WNODE\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff566372)不同于前面的结构，它用于将传递的数据块，可能包括动态实例名称和可能的不同大小的多个实例。

下图显示了一个 IRP 缓冲区，其中包含的框图**WNODE\_所有\_数据**驱动程序可能会在响应中返回的[ **IRP\_MN\_查询\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff551650)请求。

![说明包含 wnode irp 缓冲区的关系图\-所有\-数据](images/wnode-all-data.png)

开始在上图中的顶部：

- 上图中所述[ **WNODE\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff566375)结构的开头[ **WNODE\_所有\_数据** ](https://msdn.microsoft.com/library/windows/hardware/ff566372)中包含**WnodeHeader**成员。 **WnodeHeader.Buffersize**并**WnodeHeader.Guid**指示的大小**WNODE\_所有\_数据**和数据块的 GUID 分别。

  在此示例中，设置 WMI **WnodeHeader.Flags**以指示此结构是**WNODE\_所有\_数据**和与动态实例是否已注册的数据块名称 （也就是说，WMI 清除 WNODE\_标志\_静态\_实例\_名称和 WNODE\_标志\_PDO\_实例\_名称)。 在输出时，驱动程序设置 WNODE\_标志\_FIXED\_实例\_SIZE 来指示所有实例都是相同的大小。

- WMI 集**DataBlockOffset**以指示从缓冲区的开头到实例数据的第一个字节的偏移量。 （该驱动程序必须更改此值。） 在此示例中，实例数据将遵循在实例名称**OffsetInstanceNameOffsets**。

- 驱动程序集**InstanceCount**以指示要返回的实例数。

- **WNODE\_* XXX*** 的数据始终使用动态实例名称的块包含实例名称字符串。 因为此示例使用动态实例名称**OffsetInstanceNameOffsets**指示从缓冲区开头的偏移量到缓冲区中的动态实例名称数组的偏移量。

- **FixedInstanceSize**指示驱动程序返回每个实例中的数据的字节数。 如果此数据块的实例的大小不同，该驱动程序会清除 WNODE\_标志\_FIXED\_实例\_大小**WnodeHeader.Flags**并设置**OffsetInstanceDataAndLength**的数组**OFFSETINSTANCEDATAANDLENGTH**结构，而不是设置该实例中每个指定的字节数和一个实例的数据的偏移量**FixedInstanceSize**。

有关详细信息**WNODE\_* XXX*** 结构，请参阅[系统结构](https://msdn.microsoft.com/library/windows/hardware/ff564540)。

 

 




