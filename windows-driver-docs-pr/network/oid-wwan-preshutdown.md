---
title: OID_WWAN_PRESHUTDOWN
description: 发送 OID_WWAN_PRESHUTDOWN 时，通知调制解调器系统正在进入关闭阶段，并且调制解调器应完成其操作，使其能够正常关闭。
ms.assetid: B00A2D70-64E0-4686-92FC-D4095BDD713B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PRESHUTDOWN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d2799e96843312f4df1964beb413defec873fc3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843808"
---
# <a name="oid_wwan_preshutdown"></a>OID\_WWAN\_PRESHUTDOWN


将发送 OID\_WWAN\_PRESHUTDOWN 以通知调制解调器系统正在进入关闭阶段，并且调制解调器应完成其操作，使其能够正常关闭。 它仅与物理 MBB 适配器对应的端口号一起发送。 支持多个 PDP 上下文的虚拟适配器不应接收此 OID。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初返回**NDIS\_状态\_指示\_需要**原始请求，稍后发送[**ndis\_状态\_WWAN\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state)当 MBB 驱动程序在关机前完成所有必需的调制解调器操作时，PRESHUTDOWN\_状态通知。 Set 请求具有一个[**NDIS\_WWAN\_集\_PRESHUTDOWN\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)结构。

如果不支持此操作，微型端口驱动程序应返回**NDIS\_状态\_不\_支持**。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>从 Windows 10 版本1511开始可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[ **\_WWAN\_PRESHUTDOWN\_状态的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preshutdown-state)

[**NDIS\_WWAN\_集\_PRESHUTDOWN\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)

 

 




