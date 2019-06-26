---
title: OID_WWAN_PRESHUTDOWN
description: OID_WWAN_PRESHUTDOWN 发送通知调制解调器，系统即将进入关机阶段和调制解调器应完成其操作，因此它可以正确关闭。
ms.assetid: B00A2D70-64E0-4686-92FC-D4095BDD713B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PRESHUTDOWN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b69613062c61a4fb24c7478fd5169e0ebd1d72b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383210"
---
# <a name="oidwwanpreshutdown"></a>OID\_WWAN\_PRESHUTDOWN


OID\_WWAN\_PRESHUTDOWN 发送通知调制解调器，系统即将进入关机阶段和调制解调器应完成其操作，因此它可以正确关闭。 它是仅发送与对应于物理 MBB 适配器的端口号。 支持多个 PDP 上下文的虚拟适配器不应在收到此 OID。

不支持查询请求。

微型端口驱动程序必须处理最初，以异步方式返回的集请求**NDIS\_状态\_指示\_必需**向原始请求及更高版本发送[**NDIS\_状态\_WWAN\_PRESHUTDOWN\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state)状态通知时 MBB 驱动程序已完成所有必要的调制解调器操作在之前关闭。 设置请求已[ **NDIS\_WWAN\_设置\_PRESHUTDOWN\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)结构。

微型端口驱动程序应返回**NDIS\_状态\_不\_支持**如果它们不支持此操作。

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
<td><p>从 Windows 10，版本 1511年开始可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_状态\_WWAN\_PRESHUTDOWN\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state)

[**NDIS\_WWAN\_设置\_PRESHUTDOWN\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)

 

 




