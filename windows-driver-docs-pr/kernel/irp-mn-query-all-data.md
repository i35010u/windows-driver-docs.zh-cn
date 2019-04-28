---
title: IRP_MN_QUERY_ALL_DATA
description: 支持 WMI 的所有驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 9d4e1c2e-73ad-4fc3-99e6-391a64edfa5c
keywords:
- IRP_MN_QUERY_ALL_DATA Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 5a3caa66f4b6b68b32f7fd712619b76492cf73f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342706"
---
# <a name="irpmnqueryalldata"></a>IRP\_MN\_查询\_所有\_数据


支持 WMI 的所有驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://msdn.microsoft.com/library/windows/hardware/ff546968)。

如果驱动程序调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)处理**IRP\_MN\_查询\_所有\_数据**请求中的 WMI打开调用该驱动程序[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将此 IRP 发送到给定的数据块的所有实例的查询。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**中 IRP 的驱动程序的 I/O 堆栈位置指向应该对请求进行响应的驱动程序的设备对象。

**Parameters.WMI.DataPath**指向标识数据块的 GUID。

**Parameters.WMI.BufferSize**指示在非分页缓冲区的最大大小**Parameters.WMI.Buffer**，它从请求可以接收输出数据。 缓冲区大小必须大于或等于**sizeof**(**WNODE\_所有\_数据**) 以及实例名称和要返回的所有实例的数据的大小。

## <a name="output-parameters"></a>输出参数


如果该驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，WMI 会填写**WNODE\_所有\_数据**通过调用驱动程序的*DpWmiQueryDataBlock*例程一次为每个块由驱动程序注册。

否则，该驱动程序会填写[ **WNODE\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff566372)结构在**Parameters.WMI.Buffer** ，如下所示：

-   设置**WnodeHeader.BufferSize**到整个的字节数**WNODE\_所有\_数据**才能返回，设置**WnodeHeader.Timestamp**返回的值**KeQuerySystemTime**，并设置**WnodeHeader.Flags**以适合要返回的数据。

-   集**InstanceCount**到要返回的实例数。

-   如果应用程序块使用动态实例名称，设置**OffsetInstanceNameOffsets**以字节为单位从开头的偏移量**WNODE\_所有\_数据**指向的位置的 ULONG 数组偏移量开始。 此数组中的每个元素是从偏移量**WNODE\_所有\_数据**到每个动态实例名称的存储位置。 每个动态实例名称将被视为其中计数是 Unicode 字符串后跟 USHORT 计数的 Unicode 字符串。 计数不包括任何可能是 Unicode 字符串的一部分的终止 null 字符。 如果 Unicode 字符串包含终止 null 字符，必须仍在此 null 字符范围内中建立的大小**WNodeHeader.BufferSize**。

-   如果所有实例都是相同的大小：
    -   设置 WNODE\_标志\_FIXED\_实例\_大小**WnodeHeader.Flags** ，并设置**FixedInstanceSize**为该大小，以字节为单位。
    -   将实例数据开始写入**DataBlockOffset**，与填充，以便每个实例与 8 字节边界对齐。 例如，如果**FixedInstanceSize**为 6 时，驱动程序会添加 2 个字节的实例之间的填充。
-   如果实例在大小方面有所不同：
    -   清除 WNODE\_标志\_FIXED\_实例\_大小**WnodeHeader.Flags** ，并将写入的数组**InstanceCount** **OFFSETINSTANCEDATAANDLENGTH**结构开始**OffsetInstanceDataAndLength**。 每个**OFFSETINSTANCEDATAANDLENGTH**结构以字节为单位从开头指定偏移量**WNODE\_所有\_数据**到每个数据的起始位置的结构实例和数据的长度。 **DataBlockOffset**不使用。

    -   将以下的最后一个元素的实例数据写入**OffsetInstanceDataAndLength**数组，加上填充，以便每个实例与 8 字节边界对齐。

如果在缓冲区**Parameters.WMI.Buffer**太小，若要接收的所有数据，所需大小在驱动程序填充[ **WNODE\_过\_小**](https://msdn.microsoft.com/library/windows/hardware/ff566379)结构，在**Parameters.WMI.Buffer**。 如果缓冲区小于**sizeof**(**WNODE\_过\_小**)，该驱动程序将 IRP 失败并返回状态\_缓冲区\_过\_小。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_缓冲区\_过\_小

状态\_WMI\_GUID\_不\_找到

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**写入的缓冲区的字节数**Parameters.WMI.Buffer**。

<a name="operation"></a>操作
---------

驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://msdn.microsoft.com/library/windows/hardware/ff546968)。

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，例程调用的驱动程序[ *DpWmiQueryDataBlock* ](https://msdn.microsoft.com/library/windows/hardware/ff544096)例程。

如果驱动程序处理**IRP\_MN\_查询\_所有\_数据**请求时，才应该这样做**Parameters.WMI.ProviderId**指向相同设备对象，该驱动程序传递给[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

之前处理请求，该驱动程序必须确定是否**Parameters.WMI.DataPath**指向该驱动程序支持的 GUID。 如果不是，该驱动程序必须失败 IRP，并返回状态\_WMI\_GUID\_不\_找到。

如果该驱动程序支持的数据块，它必须执行以下操作：

-   确认**Parameters.WMI.BufferSize**指定足够大，以接收该驱动程序将返回的所有数据的缓冲区。

-   填写[ **WNODE\_所有\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff566372)结构在**Parameters.WMI.Buffer**与该数据块的所有实例的数据。

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


[*DpWmiQueryDataBlock*](https://msdn.microsoft.com/library/windows/hardware/ff544096)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**KeQuerySystemTime**](https://msdn.microsoft.com/library/windows/hardware/ff553068)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

[**WNODE\_ALL\_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff566372)

 

 




