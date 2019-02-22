---
title: OID_WWAN_DELETE_MAC
description: OID_WWAN_DELETE_MAC 请求微型端口驱动程序，若要删除 NDIS_WWAN_MAC_INFO 参数中指定的 NDIS 端口。
ms.assetid: 3C992E0D-132E-4687-B38E-31409E1A9F54
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DELETE_MAC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 02fbe5937ce640e9afb74032fd19cbf9553f8427
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525769"
---
# <a name="oidwwandeletemac"></a>OID\_WWAN\_DELETE\_MAC


OID\_WWAN\_删除\_MAC 请求微型端口驱动程序，若要删除 NDIS 中指定的 NDIS 端口\_WWAN\_MAC\_信息参数。 NDIS 端口应已创建以前使用[OID\_WWAN\_创建\_MAC](oid-wwan-create-mac.md)。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_PENDING 到原始请求和更高版本完成该请求与 NDIS\_状态\_成功。

不支持查询请求。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须处理请求以删除 （停用） 的端口 NDIS 以异步方式以防止死锁。

OID\_WWAN\_删除\_发送若要删除的默认端口 MAC 请求将失败，NDIS 状态错误代码 NDIS\_状态\_无效\_端口。

一旦收到 OID\_WWAN\_删除\_MAC 请求时，如果它已不已被停用，微型端口驱动程序应停用与端口相关联的 PDP 上下文。 这是因为可能发生意外删除事件。 在此类时停用 PDP 上下文将确保调制解调器和微型端口驱动程序保持处于良好状态。

当驱动程序收到意外删除，驱动程序块，并取消所有后续的 Oid。 这意味着该驱动程序筛选出 OID\_WWAN\_删除\_即使 Windows 发送具有 OID 调用 MAC\_WWAN\_删除\_作为的一部分的 MAC [ *筛选器\_分离*](https://msdn.microsoft.com/library/windows/hardware/ff549918)调用。

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
<td><p>在 Windows 8.1 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_CREATE\_MAC](oid-wwan-create-mac.md)

 

 




