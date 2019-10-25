---
title: IRP_MN_QUERY_ALL_DATA
description: 支持 WMI 的所有驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 9d4e1c2e-73ad-4fc3-99e6-391a64edfa5c
keywords:
- IRP_MN_QUERY_ALL_DATA 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: d1ef368fe4437e52f9bc02061de0bb051cc23677
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838578"
---
# <a name="irp_mn_query_all_data"></a>IRP\_MN\_查询\_所有\_数据


支持 WMI 的所有驱动程序都必须处理此 IRP。 驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理**IRP\_MN\_QUERY\_所有\_数据**请求，则 WMI 反过来会调用该驱动程序的[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)发送时间
---------

WMI 发送此 IRP 以查询给定数据块的所有实例。

WMI 在任意线程上下文中以 IRQL = 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


IRP 中的**参数. ProviderId。** IRP 中的驱动程序的 i/o 堆栈位置指向应响应该请求的驱动程序的设备对象。

**数据路径**指向标识数据块的 GUID。

**参数. BufferSize**指示非分页缓冲区的最大大小，该缓冲区位于**参数. buffer**，后者接收来自请求的输出数据。 缓冲区大小必须大于或等于**sizeof**（**WNODE\_所有\_数据**）加上所有要返回的实例的实例名称和数据的大小。

## <a name="output-parameters"></a>输出参数


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，wmi 将通过为驱动程序注册的每个块调用驱动程序的*DpWmiQueryDataBlock*例程，来填充**WNODE\_所有\_的数据**。

否则，驱动程序**将在** [ **\_WNODE 中填充所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)结构，如下所示：

-   将**WnodeHeader**设置为整个 WNODE\_要返回的**所有\_数据**的字节数，将**WnodeHeader**设置为**KeQuerySystemTime**返回的值，并设置**WnodeHeader。** 适用于要返回的数据。

-   将**InstanceCount**设置为要返回的实例数。

-   如果块使用动态实例名称，则会将**OffsetInstanceNameOffsets**的偏移量设置为以字节为单位的偏移量（以字节为单位） **\_所有\_数据**到从 ULONG 偏移量开始的数组。 此数组中的每个元素都是从**WNODE\_所有\_数据**到存储每个动态实例名称的位置的偏移量。 每个动态实例名称都存储为计数的 Unicode 字符串，其中计数为 USHORT，后跟 Unicode 字符串。 此计数不包括任何可以作为 Unicode 字符串的一部分的终止 null 字符。 如果 Unicode 字符串确实包含终止 null 字符，则此 null 字符必须仍在**WNodeHeader**中建立的大小内。

-   如果所有实例大小相同：
    -   将 WNODE\_标记\_固定\_\_实例设置为**WnodeHeader** ，并将**FixedInstanceSize**设置为该大小（以字节为单位）。
    -   写入从**DataBlockOffset**开始的实例数据，使用填充，使每个实例与8字节边界对齐。 例如，如果**FixedInstanceSize**为6，则驱动程序会在实例之间添加2个字节的填充。
-   如果实例大小不同：
    -   清除 WNODE\_标记\_固定\_实例在**WnodeHeader**中\_大小并写入从 OFFSETINSTANCEDATAANDLENGTH 开始的**InstanceCount** **OFFSETINSTANCEDATAANDLENGTH**结构的数组. 每个**OFFSETINSTANCEDATAANDLENGTH**结构都以字节为单位指定每个实例的数据开始处的偏移量（以字节为单位） **\_\_** 数据的长度。 不使用**DataBlockOffset** 。

    -   在**OffsetInstanceDataAndLength**数组的最后一个元素后写入实例数据，加上填充，使每个实例与8字节边界对齐。

如果\_WNODE 中的缓冲区太小，无法接收所有数据，则驱动程序会在**参数. buffer** [ **\_小型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)结构中填充所需**的大小。** 如果缓冲区小于**sizeof**（**WNODE\_太小\_** ），则该驱动程序将无法 IRP，并\_缓冲区返回状态\_\_太小。

## <a name="io-status-block"></a>I/O 状态块


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp&gt;IoStatus**和**irp-&gt;IoStatus** 。

否则，驱动程序会将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS 或适当的错误状态，如下所示：

状态\_缓冲区\_太小\_

找不到\_WMI\_GUID\_的状态\_

成功时，驱动程序将**Irp&gt;IoStatus**设置为写入**缓冲区中的字节数。**

<a name="operation"></a>操作
---------

驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则该例程将调用驱动程序的[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程。

如果驱动程序处理**IRP\_MN\_QUERY\_所有\_数据**请求，则仅当[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)指向驱动程序传递给的同一设备对象时，才应执行此**操作。** 否则，驱动程序必须将请求转发到下一个较低版本的驱动程序。

在处理请求之前，驱动程序必须确定**数据路径**是否指向驱动程序支持的 GUID。 否则，驱动程序必须失败 IRP 并返回状态\_WMI\_GUID\_找不到\_。

如果驱动程序支持数据块，则必须执行以下操作：

-   验证**Parameters. BufferSize**是否指定了足以接收驱动程序将返回的所有数据的缓冲区。

-   使用[**WNODE\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)结构中的所有数据**块的所有**实例的数据。

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


[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)

[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_所有\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)

 

 




