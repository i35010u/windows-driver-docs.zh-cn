---
title: IRP_MN_QUERY_ALL_DATA
description: 支持 WMI 的所有驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 9d4e1c2e-73ad-4fc3-99e6-391a64edfa5c
keywords:
- IRP_MN_QUERY_ALL_DATA 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 6735f6a879c8cb01a3d3e582dd5d3e1a67257887
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189523"
---
# <a name="irp_mn_query_all_data"></a>IRP \_ MN \_ 查询 \_ 所有 \_ 数据


支持 WMI 的所有驱动程序都必须处理此 IRP。 驱动程序可以通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 或处理 IRP 本身来处理 wmi irp，如 [处理 WMI 请求](./handling-wmi-requests.md)中所述。

如果驱动程序调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 来处理 **IRP \_ MN \_ 查询 \_ 所有 \_ 数据** 请求，WMI 反过来就会调用该驱动程序的 [*DpWmiQueryDataBlock*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback) 例程。

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ 系统 \_ 控件**](irp-mj-system-control.md)

<a name="when-sent"></a>发送时间
---------

WMI 发送此 IRP 以查询给定数据块的所有实例。

WMI \_ 在任意线程上下文中以 IRQL = 被动级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


IRP 中的**参数. ProviderId。** IRP 中的驱动程序的 i/o 堆栈位置指向应响应该请求的驱动程序的设备对象。

**数据路径** 指向标识数据块的 GUID。

**参数. BufferSize** 指示非分页缓冲区的最大大小，该缓冲区位于 **参数. buffer**，后者接收来自请求的输出数据。 缓冲区大小必须大于或等于 **sizeof** (**WNODE \_ 所有 \_ 数据**) 加上所有要返回的实例的实例名称和数据的大小。

## <a name="output-parameters"></a>输出参数


如果驱动程序通过调用[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，wmi 将通过为驱动程序注册的每个块调用驱动程序的*DpWmiQueryDataBlock*例程，来填充**WNODE 的 \_ 所有 \_ 数据**。

否则，驱动程序将在 WNODE 中填充 [** \_ 所有 \_ 数据**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data) 结构 **，如下** 所示：

-   将**WnodeHeader**设置为要返回的整个 WNODE 的字节数，将**WnodeHeader**设置为**KeQuerySystemTime**返回的值，并将**WnodeHeader**设置为适用于要返回的数据。 ** \_ \_ **

-   将 **InstanceCount** 设置为要返回的实例数。

-   如果块使用动态实例名称，则会将 **OffsetInstanceNameOffsets** 设置为 **WNODE \_ 所有 \_ 数据** 开始处的偏移量（以字节为单位）。 此数组中的每个元素都是 WNODE 的偏移量，其中的 ** \_ 所有 \_ 数据** 都存储在其中。 每个动态实例名称都存储为计数的 Unicode 字符串，其中计数为 USHORT，后跟 Unicode 字符串。 此计数不包括任何可以作为 Unicode 字符串的一部分的终止 null 字符。 如果 Unicode 字符串确实包含终止 null 字符，则此 null 字符必须仍在 **WNodeHeader**中建立的大小内。

-   如果所有实例大小相同：
    -   在 \_ WnodeHeader 中设置 WNODE 标记 \_ 固定 \_ 实例大小， \_ 并将**FixedInstanceSize**设置为该大小（以字节为单位）。 **WnodeHeader.Flags**
    -   写入从 **DataBlockOffset**开始的实例数据，使用填充，使每个实例与8字节边界对齐。 例如，如果 **FixedInstanceSize** 为6，则驱动程序会在实例之间添加2个字节的填充。
-   如果实例大小不同：
    -   清除 \_ \_ \_ WNODEHEADER 中的 WNODE 标记固定实例 \_ 大小，并写入从**OFFSETINSTANCEDATAANDLENGTH**开始的**InstanceCount** **OFFSETINSTANCEDATAANDLENGTH**结构的数组。 **WnodeHeader.Flags** 每个**OFFSETINSTANCEDATAANDLENGTH**结构都指定从 WNODE 的开头到每个实例的数据开头的偏移量（以字节为单位）和数据的长度。 ** \_ \_ ** 不使用**DataBlockOffset** 。

    -   在 **OffsetInstanceDataAndLength** 数组的最后一个元素后写入实例数据，加上填充，使每个实例与8字节边界对齐。

如果位于**参数. buffer**的缓冲区太小而无法接收所有数据，则驱动程序会在 WNODE 中的**参数** [** \_ 太 \_ 小**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)的结构中填充所需的大小。 如果缓冲区小于 **sizeof** (**WNODE \_ 太 \_ 小**) ，则该驱动程序将失败 IRP 并返回状态 \_ 缓冲区 \_ 太 \_ 小。

## <a name="io-status-block"></a>I/o 状态块


如果驱动程序通过调用[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp- &gt; IoStatus**和**irp- &gt; IoStatus。**

否则，驱动程序会将 **Irp- &gt; IoStatus** 设置为状态 \_ 成功，或设置为适当的错误状态，如下所示：

状态 \_ 缓冲区 \_ 太 \_ 小

\_ \_ \_ 找不到 WMI \_ GUID 状态

成功时，驱动程序将**Irp- &gt; IoStatus**设置为写入**缓冲区中的字节数。**

<a name="operation"></a>操作
---------

驱动程序可以通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 或处理 IRP 本身来处理 wmi irp，如 [处理 WMI 请求](./handling-wmi-requests.md)中所述。

如果驱动程序通过调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的 [*DpWmiQueryDataBlock*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback) 例程。

如果驱动程序处理**IRP \_ MN \_ 查询 \_ 所有 \_ 数据**请求，则仅当 IoWMIRegistrationControl 指向驱动程序传递给[**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)的同一设备对象时，才应执行此**操作。** 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

在处理请求之前，驱动程序必须确定 **数据路径** 是否指向驱动程序支持的 GUID。 如果不是，则驱动程序必须失败 IRP 并返回 \_ 状态 \_ WMI \_ GUID \_ 找不到。

如果驱动程序支持数据块，则必须执行以下操作：

-   验证 **Parameters. BufferSize** 是否指定了足以接收驱动程序将返回的所有数据的缓冲区。

-   在 WNODE 的[** \_ 所有 \_ 数据**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)结构中填写**Parameters.WMI.Buffer**数据块的所有实例的数据。

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
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DpWmiQueryDataBlock*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)

[**WMILIB \_ 上下文**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE \_ 所有 \_ 数据**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)

 

