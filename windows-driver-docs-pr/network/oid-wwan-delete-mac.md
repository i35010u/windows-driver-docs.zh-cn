---
title: OID_WWAN_DELETE_MAC
description: OID_WWAN_DELETE_MAC 请求微型端口驱动程序删除 NDIS_WWAN_MAC_INFO 参数中指定的 NDIS 端口。
ms.assetid: 3C992E0D-132E-4687-B38E-31409E1A9F54
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DELETE_MAC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fc43a11868e9efa52bc8aa280dd618cc0233af96
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843866"
---
# <a name="oid_wwan_delete_mac"></a>OID\_WWAN\_删除\_MAC


OID\_WWAN\_DELETE\_MAC 请求微型端口驱动程序删除在 NDIS\_WWAN\_MAC\_INFO 参数中指定的 NDIS 端口。 应使用[OID\_WWAN\_创建\_MAC](oid-wwan-create-mac.md)之前创建 NDIS 端口。

微型端口驱动程序必须异步处理集请求，最初返回 NDIS\_状态\_挂起到原始请求，然后在完成请求时将 NDIS\_状态\_成功。

不支持查询请求。

<a name="remarks"></a>备注
-------

小型端口驱动程序必须处理请求以异步方式删除（停用） NDIS 端口，以防止死锁。

OID\_WWAN\_删除发送到删除默认端口的\_MAC 请求将失败，并出现 NDIS 状态错误代码 NDIS\_状态\_无效\_端口。

收到 OID\_WWAN\_删除\_MAC 请求后，如果尚未停用端口，微型端口驱动程序应停用与该端口关联的 PDP 上下文。 这是因为可能会发生意外的删除事件。 在这种情况停用 PDP 上下文将确保调制解调器和微型端口驱动程序保持良好的状态。

当驱动程序收到意外删除时，驱动程序会阻止并取消所有其他 Oid。 这意味着，即使 Windows 使用 OID 发送调用\_WWAN\_删除\_MAC 作为[*筛选器\_分离*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach)调用的一部分，驱动程序也\_WWAN\_删除\_mac。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_创建\_MAC](oid-wwan-create-mac.md)

 

 




