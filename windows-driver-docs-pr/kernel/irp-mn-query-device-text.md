---
title: IRP_MN_QUERY_DEVICE_TEXT
description: PnP 管理器使用此 IRP 获取设备的说明或位置信息。总线驱动程序必须处理其子设备的此请求，如果在总线支持此信息。 函数和筛选器驱动程序不处理此 IRP。
ms.date: 08/12/2017
ms.assetid: 07661709-8929-4567-a05f-96d995862ee6
keywords:
- IRP_MN_QUERY_DEVICE_TEXT 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: eedcf3d55e5e95ee877360a3ded21b914ffe5d45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381439"
---
# <a name="irpmnquerydevicetext"></a>IRP\_MN\_查询\_设备\_文本


PnP 管理器使用此 IRP 获取设备的说明或位置信息。

总线驱动程序必须处理其子设备的此请求，如果在总线支持此信息。 函数和筛选器驱动程序不处理此 IRP。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md) When Sent
---------

PnP 管理器将发送两个 Irp 枚举设备时： 一个查询用于查询设备描述，另一个用于查询的位置信息。

PnP 管理器将此 IRP 发送在 IRQL 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.QueryDeviceText.DeviceTextType**的成员[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构是**设备\_文本\_类型**值，该值指定所请求的字符串。 可能的值**设备\_文本\_类型**包括**DeviceTextDescription**并**DeviceTextLocationInformation**。

**Parameters.QueryDeviceText.LocaleId**是指定请求的文本的区域设置 LCID。

## <a name="output-parameters"></a>输出参数


返回在 I/O 状态块中。

## <a name="io-status-block"></a>I/O 状态块


驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态。

如果成功，总线驱动程序设置**Irp-&gt;IoStatus.Information**到驱动程序分配的包含具有所需的信息的 WCHAR 缓冲区的内存块的指针。 发生错误时，总线驱动程序设置**Irp-&gt;IoStatus.Information**为零。

<a name="operation"></a>操作
---------

强烈建议，若要返回其子设备的设备描述的总线驱动程序。 此字符串显示在**发现新硬件**弹出窗口，如果设备不存在任何 INF 匹配。

另外还建议设置总线驱动程序返回**LocationInformation**对于自己的孩子的设备，但此信息是可选的。 此字符串的格式取决于在总线。 设备管理器设备的常规属性选项卡中显示此字符串。 供应商应选择传达给用户的有用信息的字符串和技术支持人员。 例如，对于 PCI，该字符串包含总线、 设备和函数。 PC 卡，该字符串包含槽。

如果总线驱动程序对此 IRP 响应中返回的信息，它会从分页的内存分配的以 NULL 结尾的 Unicode 字符串。 PnP 管理器不再需要时释放该字符串。

如果设备不提供说明或位置的信息，将设备的父总线驱动程序会完成 IRP ([**IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) 而无需修改**Irp-&gt;IoStatus.Status**或**Irp-&gt;IoStatus.Information**。

函数和筛选器驱动程序不处理此 IRP;它们将其传递给下一个较低驱动程序和无变化**Irp-&gt;IoStatus**。

对于不同的区域设置支持不同的文本字符串的总线驱动程序应该能够处理请求的设备不显式支持的语言。 在这种情况下，总线驱动程序应返回最接近的匹配的区域设置或应回退和返回某些相应支持的区域设置字符串。

请参阅[插](https://msdn.microsoft.com/library/windows/hardware/ff547125)处理的常规规则[即插即用次要 Irp](plug-and-play-minor-irps.md)。

**发送此 IRP**

保留供系统使用。 驱动程序必须发送此 IRP。

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

 

 




