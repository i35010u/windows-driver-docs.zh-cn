---
title: OID_WWAN_CREATE_MAC
description: OID_WWAN_CREATE_MAC 要求微型端口驱动程序创建新的 NDIS 端口。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_CREATE_MAC 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4e3d19799aca287ea8b089d89c1e0b0247bbbed3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797979"
---
# <a name="oid_wwan_create_mac"></a>OID \_ WWAN \_ CREATE \_ MAC


OID \_ WWAN \_ CREATE \_ MAC 请求微型端口驱动程序来创建新的 NDIS 端口。 将在此新 NDIS 端口上发送针对额外 PDP 上下文的上下文激活请求。

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后用 [**ndis \_ WWAN \_ MAC \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info) 结构来完成请求，该结构指示与端口关联的 ndis 端口号和 MAC 地址。

不支持查询请求。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须处理请求以创建 (激活) 新的 NDIS 端口，以防止死锁。

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


[**NDIS \_ WWAN \_ MAC \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info)

[OID \_ WWAN \_ 删除 \_ MAC](oid-wwan-delete-mac.md)

 

