---
title: IRP_MN_ENABLE_COLLECTION
description: 注册一个或多个其数据的任何 WMI 驱动程序会阻止为可能耗时或成本高昂，收集必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: dc6c3ceb-a992-4e7b-ab25-d91c00af655a
keywords:
- IRP_MN_ENABLE_COLLECTION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: cfe736b209065dc3575f9f9642ea0183cd4e1837
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368358"
---
# <a name="irpmnenablecollection"></a>IRP\_MN\_启用\_集合


将一个或多个其数据块注册为可能很耗时，任何 WMI 驱动程序或*昂贵*到收集必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://msdn.microsoft.com/library/windows/hardware/ff546968)。

如果驱动程序调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)处理**IRP\_MN\_启用\_集合**请求时，WMI 反过来调用驱动程序的[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将发送此 IRP 请求驱动程序启动的驱动程序已注册的数据块的累积数据的开销收集。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**指向标识为其收集数据的数据块的 GUID。

## <a name="output-parameters"></a>输出参数


无。

## <a name="io-status-block"></a>I/O 状态块


如果该驱动程序通过调用来处理 IRP [ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，WMI 集**Irp-&gt;IoStatus.Status**并**Irp-&gt;IoStatus.Information** I/O 状态块中。

否则，该驱动程序设置**Irp-&gt;IoStatus.Status**于状态\_成功或相应的错误状态，如下所示：

状态\_WMI\_GUID\_不\_找到

STATUS\_INVALID\_DEVICE\_REQUEST

如果成功，驱动程序设置**Irp-&gt;IoStatus.Information**为零。

<a name="operation"></a>操作
---------

驱动程序将数据块注册为昂贵以收集设置 WMIREG\_标志\_中的昂贵**标志**的成员[ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)或[ **WMIGUIDREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565811)结构。 该驱动程序将这些结构传递到 WMI 时它会注册或更新数据块。 驱动程序需要不会累积数据的此类块，直到收到的显式请求来启动数据收集。

驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://msdn.microsoft.com/library/windows/hardware/ff546968)。

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，例程调用的驱动程序[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)例程，返回状态或\_成功如果驱动程序不会定义该例程。

如果驱动程序处理**IRP\_MN\_启用\_集合**请求本身，才应该这样做**Parameters.WMI.ProviderId**指向同一个设备对象传递给驱动程序的指针作为[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

之前处理请求，该驱动程序应确保**Parameters.WMI.DataPath**指向该驱动程序支持的 GUID。 如果未显示，该驱动程序应失败 IRP，并且返回状态\_WMI\_GUID\_不\_找到。 如果数据块是否有效，但未注册到 WMIREG\_标志\_昂贵，则驱动程序可以返回状态\_成功，并采取任何进一步的操作。

如果块有效并已注册到 WMIREG\_标志\_昂贵，驱动程序，该数据块的所有实例的数据收集。

不需要的驱动程序来检查是否为数据块已启用数据收集。 WMI 发送仅启用一个数据块后第一个数据使用者可的块的单个请求。 WMI 不会发送另一个请求以启用无有干预性禁用请求。

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


[*DpWmiFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff544094)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**IRP\_MN\_禁用\_集合**](irp-mn-disable-collection.md)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

 

 




