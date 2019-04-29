---
title: NDIS_STATUS_PORT_STATE
description: 支持 NDIS 端口的微型端口驱动程序使用 NDIS_STATUS_PORT_STATE 状态指示指示 NDIS 端口的状态变化。
ms.assetid: 28e76963-af06-4a00-83ef-14e009cf35ec
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PORT_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1b27ceec7371a06e5270b45071dcfa809274532c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362877"
---
# <a name="ndisstatusportstate"></a>NDIS\_状态\_端口\_状态


支持 NDIS 端口的微型端口驱动程序使用 NDIS\_状态\_端口\_状态状态指示，指示在 NDIS 端口的状态更改。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须在中设置的端口号**PortNumber**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构。 **StatusBuffer**此结构的成员包含一个指向[ **NDIS\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566800)结构。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff566800)

[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

 

 




