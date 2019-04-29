---
title: NDIS_STATUS_PM_CAPABILITIES_CHANGE
description: NDIS_STATUS_PM_CAPABILITIES_CHANGE 状态指示在对基础驱动程序的网络适配器的电源管理功能的更改。
ms.assetid: 28a2ed15-606a-4a40-b975-b766815a02cc
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_CAPABILITIES_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3fd5f1e2dadeb9ff4a8b2c9fbfb62fc7fc18f6d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362889"
---
# <a name="ndisstatuspmcapabilitieschange"></a>NDIS\_状态\_PM\_功能\_更改


NDIS\_状态\_PM\_功能\_更改状态指示为过量驱动程序的电源管理功能的网络适配器的更改。

<a name="remarks"></a>备注
-------

NDIS 生成 NDIS\_状态\_PM\_功能\_更改状态指示时对先前报告的电源管理功能的更新是必需的。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构包含一个指向[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构的更新的电源管理功能。

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
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




