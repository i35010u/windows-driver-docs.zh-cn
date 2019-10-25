---
title: IRP_MN_QUERY_SINGLE_INSTANCE
description: 支持 WMI 的所有驱动程序都必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 104b6b3e-aa5d-437f-8236-02e4abb1ba46
keywords:
- IRP_MN_QUERY_SINGLE_INSTANCE 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 6c558f6fabc7462cc0959a26f3f2729ecf1ae5ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827979"
---
# <a name="irp_mn_query_single_instance"></a>IRP\_MN\_QUERY\_单一\_实例


支持 WMI 的所有驱动程序都必须处理此 IRP。 驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理**IRP\_MN\_QUERY\_单一\_实例**请求，则 WMI 反过来会调用该驱动程序的[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)发送时间
---------

WMI 发送此 IRP 以查询给定数据块的单个实例。

在发送[**irp\_MN\_EXECUTE\_方法**](irp-mn-execute-method.md)之前，WMI 会将**irp\_MN\_QUERY\_单一\_实例**发送。 如果驱动程序支持**irp\_MN\_EXECUTE\_方法**，则该驱动程序必须为其方法正在执行的同一数据块提供**irp\_MN\_查询\_单\_实例**处理程序。

WMI 在任意线程上下文中以 IRQL = 被动\_级别发送此 IRP。

## <a name="input-parameters"></a>输入参数


**Parameters。 ProviderId**指向应响应请求的驱动程序的设备对象。 此指针位于 IRP 中驱动程序的 i/o 堆栈位置。

**数据路径**指向标识要查询的数据块的 GUID。

\_WNODE**指示非**分页缓冲区的最大大小，该缓冲区位于**参数.** [ **\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构中，后者用于标识要查询的实例。

## <a name="output-parameters"></a>输出参数


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，wmi 将使用驱动程序的[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程提供的数据来填充[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构。

否则，驱动程序**会在** **WNODE\_单个\_实例**结构，如下所示：

-   用输出**WNODE\_单个\_实例**结构（包括实例数据）的大小（以字节为单位）更新**WnodeHeader。** 此值应包括实例名称的长度（已填充，使实例数据在四个字边界处开始），即使正在查询的类是注册的静态实例名称，并且驱动程序编写器未在服务时显式提供该名称此 IRP。

-   将**SizeDataBlock**设置为实例数据的大小（以字节为单位）。 如果静态实例名称正在使用中，则此值不应包含实例名称的大小。

-   从**DataBlockOffset**开始将实例数据写入到**Parameters。** 驱动程序不得更改**DataBlockOffset**的输入值。

如果 WNODE 中的缓冲区太小 **，不能**接收所有数据，则驱动程序将在\_中填充所需的大小，而不[ **\_小型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)**结构。** 如果缓冲区小于**sizeof**（**WNODE\_太小\_** ），则该驱动程序将无法 IRP，并\_缓冲区返回状态\_\_太小。

## <a name="io-status-block"></a>I/O 状态块


如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 IRP，WMI 将在 i/o 状态块中设置**irp&gt;IoStatus**和**irp-&gt;IoStatus** 。

否则，驱动程序会将**Irp&gt;IoStatus**设置为 STATUS\_SUCCESS 或适当的错误状态，如下所示：

状态\_缓冲区\_太小\_

找不到\_WMI\_GUID\_的状态\_

找不到\_WMI\_实例的状态\_\_

成功时，驱动程序会将**Irp&gt;IoStatus**设置为输入到**WnodeHeader**的值。 此值包括静态实例名称的长度。

<a name="operation"></a>操作
---------

驱动程序可以通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)或处理 IRP 本身来处理 wmi irp，如[处理 WMI 请求](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)中所述。

如果驱动程序通过调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)来处理 WMI irp，则**WmiSystemControl**将调用驱动程序的[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)例程。

如果驱动程序处理**IRP\_MN\_QUERY\_单一\_实例**请求本身，则仅当**参数. ProviderId**指向与驱动程序在其调用中传递的指针相同的设备对象时，才应执行此操作。[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 否则，驱动程序必须将请求转发到设备堆栈中的下一个较低的驱动程序。

在处理请求之前，驱动程序必须确定**数据路径**是否指向驱动程序支持的 GUID。 否则，驱动程序必须失败 IRP 并返回状态\_WMI\_GUID\_找不到\_。

驱动程序负责验证所有输入值。 具体而言，如果驱动程序处理 IRP 请求本身，则必须执行以下操作：

-   对于静态名称，验证[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)结构的**InstanceIndex**成员是否在数据块的驱动程序支持的实例索引范围内。

-   对于动态名称，请验证实例名称字符串是否标识了驱动程序支持的数据块实例。

-   验证**Parameters. BufferSize**是否指定了足以接收驱动程序将返回的所有数据的缓冲区。

如果驱动程序支持数据块，它将检查输入[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)**的实例**名称，如下所示：

-   如果 WNODE\_标记\_静态\_实例在**WnodeHeader**中设置\_名称，则驱动程序使用**InstanceIndex**作为该块的静态实例名称列表中的索引。 WMI 从驱动程序注册块时提供的注册数据中获取索引。

-   如果 WNODE\_标记\_静态\_\_实例在**WnodeHeader**中为空，则驱动程序将使用**OffsetInstanceName**的偏移量在输入 WNODE 中查找实例名称字符串 **\_SINGLE\_实例**。 **OffsetInstanceName**是从结构开始到 USHORT 的偏移量（以字节为单位），该偏移量是实例名称字符串的长度（以字节为单位），包括终止 null （如果存在），后跟实例名称字符串 inUnicode.

如果驱动程序找不到指定的实例，则它必须失败 IRP 并返回状态\_WMI\_实例\_但找不到\_。 对于具有动态实例名称的实例，此状态指示该驱动程序不支持该实例。 这样，WMI 就可以继续查询其他数据访问接口，如果另一个提供程序找到该实例，但由于其他原因无法处理该请求，则会向数据使用者返回相应的错误。

如果驱动程序找到该实例并可以处理该请求，则它会在**WNODE\_单个\_实例**结构，**其中包含实例**的数据。

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
<td>Wdm .h （包括 Wdm、Ntddk 或 Ntifs）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_单个\_实例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




