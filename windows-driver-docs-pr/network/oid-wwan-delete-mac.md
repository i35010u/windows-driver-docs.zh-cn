---
title: OID_WWAN_DELETE_MAC
description: OID_WWAN_DELETE_MAC 要求微型端口驱动程序删除在 NDIS_WWAN_MAC_INFO 参数中指定的 NDIS 端口。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DELETE_MAC 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 866db341208f91c931213812d647797225e0f821
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823843"
---
# <a name="oid_wwan_delete_mac"></a>OID \_ WWAN \_ 删除 \_ MAC


OID \_ WWAN \_ 删除 \_ MAC 请求微型端口驱动程序删除在 ndis \_ WWAN \_ MAC INFO 参数中指定的 ndis 端口 \_ 。 应使用 [OID \_ WWAN \_ CREATE \_ MAC](oid-wwan-create-mac.md)之前创建 NDIS 端口。

微型端口驱动程序必须异步处理集请求，最初返回 \_ \_ 原始请求挂起的 NDIS 状态，然后在完成请求时 ndis \_ 状态为 \_ 成功。

不支持查询请求。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须处理请求以异步方式删除 (停用) NDIS 端口，以防止死锁。

OID \_ WWAN \_ 删除 \_ MAC 请求发送到删除默认端口将失败，并出现 ndis 状态错误代码 ndis \_ 状态 \_ 无效 \_ 端口。

接收到 OID \_ WWAN \_ 删除 \_ MAC 请求后，微型端口驱动程序应停用与该端口关联的 PDP 上下文（如果尚未停用）。 这是因为可能会发生意外的删除事件。 在这种情况停用 PDP 上下文将确保调制解调器和微型端口驱动程序保持良好的状态。

当驱动程序收到意外删除时，驱动程序会阻止并取消所有其他 Oid。 这意味着， \_ \_ \_ 即使 Windows 在 \_ \_ \_ [*筛选器 \_ 分离*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 调用过程中发送具有 oid wwan 删除 mac 的调用，驱动程序也会筛选出 oid wwan 删除 mac。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WWAN \_ CREATE \_ MAC](oid-wwan-create-mac.md)

 

