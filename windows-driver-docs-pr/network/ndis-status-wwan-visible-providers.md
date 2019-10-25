---
title: NDIS_STATUS_WWAN_VISIBLE_PROVIDERS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_VISIBLE_PROVIDERS 通知来通知 MB 服务完成 OID_WWAN_VISIBLE_PROVIDERS \ 160; 个查询请求。
ms.assetid: 57e79d45-536a-4ab9-8cc0-0408d722b6f7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_VISIBLE_PROVIDERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 065d9decdd973639a99a395db3e253a1c3ff54ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834648"
---
# <a name="ndis_status_wwan_visible_providers"></a>\_WWAN\_可见\_提供程序的 NDIS\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_可见的\_提供程序通知来通知 MB 服务完成[OID\_提供程序](oid-wwan-visible-providers.md)\_查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_可见\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)结构。

<a name="remarks"></a>备注
-------

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_可见\_提供程序](oid-wwan-visible-providers.md)

[**NDIS\_WWAN\_可见\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)

 

 




