---
title: NDIS_STATUS_PORT_STATE
description: 支持 NDIS 端口的微型端口驱动程序使用 NDIS_STATUS_PORT_STATE 状态指示指示 NDIS 端口的状态变化。
ms.assetid: 28e76963-af06-4a00-83ef-14e009cf35ec
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PORT_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5d2bace5b512b2daae506f60443335fd95fee0a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368533"
---
# <a name="ndisstatusportstate"></a>NDIS\_状态\_端口\_状态


支持 NDIS 端口的微型端口驱动程序使用 NDIS\_状态\_端口\_状态状态指示，指示在 NDIS 端口的状态更改。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须在中设置的端口号**PortNumber**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构。 **StatusBuffer**此结构的成员包含一个指向[ **NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)结构。

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


[**NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_state)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

 

 




