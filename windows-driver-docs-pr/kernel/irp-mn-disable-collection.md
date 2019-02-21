---
title: IRP_MN_DISABLE_COLLECTION
description: 将一个或多个其数据块注册为昂贵收集任何 WMI 驱动程序必须处理此 IRP。
ms.date: 08/12/2017
ms.assetid: de375d56-880e-4534-acab-8d0685f45ebe
keywords:
- IRP_MN_DISABLE_COLLECTION 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 4a6141a08ca3a17dcb295224f888888a3a3dd797
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523082"
---
# <a name="irpmndisablecollection"></a>IRP\_MN\_禁用\_集合


将一个或多个其数据块注册为昂贵收集任何 WMI 驱动程序必须处理此 IRP。 驱动程序可以处理 WMI Irp 通过调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)或通过处理 IRP 本身，如中所述[处理 WMI 请求](https://msdn.microsoft.com/library/windows/hardware/ff546968)。

如果驱动程序调用[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)处理**IRP\_MN\_禁用\_集合**请求时，WMI 反过来调用该驱动程序[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)例程。

<a name="major-code"></a>主代码
----------

[**IRP\_MJ\_系统\_控件**](irp-mj-system-control.md)时发送
---------

WMI 将发送此 IRP 请求以停止该驱动程序注册为成本高昂，若要收集的数据块以及哪些数据收集已启用的累积数据的驱动程序。

WMI 将此 IRP 发送在 IRQL = 被动\_级别在任意线程上下文中。

## <a name="input-parameters"></a>输入参数


**Parameters.WMI.ProviderId**指向应该对请求进行响应的驱动程序的设备对象。 此指针位于 IRP 中的驱动程序的 I/O 堆栈位置。

**Parameters.WMI.DataPath**指向标识哪些数据应停止进行累积的数据块的 GUID。

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

驱动程序将数据块注册为昂贵以收集设置 WMIREG\_标志\_中的昂贵**标志**的成员[ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)或[ **WMIGUIDREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565811)时它将注册或更新数据块，该驱动程序将传递到 WMI 的结构。 驱动程序需要不会累积数据的此类块，直到收到的显式请求，以启用收集。

如果驱动程序通过调用来处理 WMI Irp [ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)，例程调用的驱动程序[ *DpWmiFunctionControl* ](https://msdn.microsoft.com/library/windows/hardware/ff544094)例程，返回状态或\_成功如果驱动程序不会定义该例程。

如果驱动程序处理**IRP\_MN\_禁用\_集合**请求本身，才应该这样做**Parameters.WMI.ProviderId**指向同一个设备对象传递给驱动程序的指针作为[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)。 否则，该驱动程序必须将请求转发到下一步低驱动程序。

之前处理请求，该驱动程序必须确定是否**Parameters.WMI.DataPath**指向该驱动程序支持的 GUID。 如果不是，该驱动程序必须失败 IRP，并返回状态\_WMI\_GUID\_不\_找到。 如果数据块是否有效，但未注册到 WMIREG\_标志\_昂贵，则驱动程序可以返回状态\_成功，并采取任何进一步的操作。

不需要的驱动程序来检查是否因为时最后一个数据使用者禁用块所收集 WMI 数据块的单个禁用请求将发送已禁用数据收集。 WMI 不会发送另一个没有启用的干预请求禁用请求。

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
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*DpWmiFunctionControl*](https://msdn.microsoft.com/library/windows/hardware/ff544094)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**IRP\_MN\_ENABLE\_COLLECTION**](irp-mn-enable-collection.md)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)

[**WMIGUIDREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565811)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

 

 




