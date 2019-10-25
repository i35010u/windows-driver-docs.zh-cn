---
title: OID_WWAN_NETWORK_IDLE_HINT
description: OID_WWAN_NETWORK_IDLE_HINT 将提示发送到网络接口，该接口涉及到该接口上的数据是否应为活动或空闲。
ms.assetid: 1FE758C1-543A-45B4-A377-336A1307689F
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_NETWORK_IDLE_HINT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 939db61fdaa8139b7363a5ba8515161016e22d56
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843827"
---
# <a name="oid_wwan_network_idle_hint"></a>OID\_WWAN\_NETWORK\_IDLE\_提示


OID\_WWAN\_NETWORK\_IDLE\_提示将提示发送到网络接口，该接口涉及到该接口上的数据是否应为活动或空闲。 网络服务使用试探法来确定何时向接口发送此请求，通常在其估计时间段内会减少网络流量或系统进入空闲状态（如连接待机）的时间。 网络接口可以将此作为试探法的输入，以实现 "fast 休眠期间" 之类的过程。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后用[**NDIS\_WWAN\_网络完成请求\_空闲\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)结构，指示网络空闲提示。

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
<td><p>适用于 windows 10 及更高版本的 Windows。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_NETWORK\_IDLE\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)

 

 




