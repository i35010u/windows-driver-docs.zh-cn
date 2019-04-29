---
title: NDIS_STATUS_PM_WAKE_REASON
description: NDIS_STATUS_PM_WAKE_REASON 状态指示提供了有关唤醒事件时生成的网络适配器的信息。
ms.assetid: 0CF29C9B-4AAA-473D-A3E8-C1E9530B595E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_WAKE_REASON 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e713e87cc13c2114fe10d4223f17b18779876463
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362883"
---
# <a name="ndisstatuspmwakereason"></a>NDIS\_状态\_PM\_唤醒\_原因


**NDIS\_状态\_PM\_唤醒\_原因**状态指示提供有关唤醒事件时生成的网络适配器的信息。

<a name="remarks"></a>备注
-------

从开始 NDIS 6.30，微型端口驱动程序发出的 NDIS 状态指示**NDIS\_状态\_PM\_唤醒\_原因**。 此状态指示通知 NDIS 和生成的网络适配器的唤醒事件的原因有关的基础驱动程序。

如果微型端口驱动程序支持这种类型的状态指示，微型端口驱动程序必须发出**NDIS\_状态\_PM\_唤醒\_原因**状态指示如果网络适配器生成唤醒信号。 该驱动程序执行此时它正在处理的 OID 集请求[OID\_PNP\_设置\_POWER](https://msdn.microsoft.com/library/windows/hardware/ff569780)适配器到全功率状态的转换。

当微型端口驱动程序将此状态指示时，它会设置**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)为指向的结构[ **NDIS\_PM\_唤醒\_原因**](https://msdn.microsoft.com/library/windows/hardware/hh451605)结构。

详细了解如何发出**NDIS\_状态\_PM\_唤醒\_原因**指示，请参阅[发出 NDIS 唤醒原因状态指示](https://msdn.microsoft.com/library/windows/hardware/hh463944).

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_PM\_WAKE\_REASON**](https://msdn.microsoft.com/library/windows/hardware/hh451605)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




