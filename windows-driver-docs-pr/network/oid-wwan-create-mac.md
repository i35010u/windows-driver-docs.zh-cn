---
title: OID_WWAN_CREATE_MAC
description: OID_WWAN_CREATE_MAC 请求微型端口驱动程序创建新的 NDIS 端口。
ms.assetid: 4EF98858-86CD-409B-BE41-E57B24158609
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_CREATE_MAC 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f32d589fa027b401361f2a3d7de66b9fa550e0c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843868"
---
# <a name="oid_wwan_create_mac"></a>OID\_WWAN\_创建\_MAC


OID\_WWAN\_创建\_MAC 请求微型端口驱动程序来创建新的 NDIS 端口。 将在此新 NDIS 端口上发送针对额外 PDP 上下文的上下文激活请求。

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后用[**NDIS\_WWAN\_MAC 来完成请求\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info)结构，指示与端口关联的 NDIS 端口号和 MAC 地址。

不支持查询请求。

<a name="remarks"></a>备注
-------

小型端口驱动程序必须处理请求以异步方式创建（激活）新的 NDIS 端口，以防止死锁。

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


[**NDIS\_WWAN\_MAC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_mac_info)

[OID\_WWAN\_删除\_MAC](oid-wwan-delete-mac.md)

 

 




