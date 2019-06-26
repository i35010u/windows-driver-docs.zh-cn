---
title: NDIS_STATUS_MEDIA_CONNECT
description: NDIS_STATUS_MEDIA_CONNECT 状态指示设备的网络连接的状态已从断开连接更改为已连接。
ms.assetid: de03d265-c8bf-4b7d-bfff-f583fcf08904
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_MEDIA_CONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4bdc7fb6c0ff013105d9d1b2cc50cb3171706416
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383265"
---
# <a name="ndisstatusmediaconnect"></a>NDIS\_状态\_媒体\_连接


NDIS\_状态\_媒体\_CONNECT 状态指示设备的网络连接的状态已更改从断开连接到已连接。 例如，设备将连接 （适用于无线设备） 的访问点的范围内时或当用户连接设备的网络电缆。

<a name="remarks"></a>备注
-------

NDIS 转换 NDIS\_状态\_媒体\_连接到状态指示[ **NDIS\_状态\_链接\_状态**](ndis-status-link-state.md)过量 NDIS 6.0 驱动程序的状态指示。

NDIS 5。*x*和更早的微型端口驱动程序指示[ **NDIS\_状态\_媒体\_断开连接**](ndis-status-media-disconnect.md)时微型端口驱动程序的状态确定网络连接已丢失。 该驱动程序当恢复连接时，指示 NDIS\_状态\_媒体\_连接状态。

详细了解 NDIS\_状态\_媒体\_连接，请参阅[，该值指示连接状态 (NDIS 5.1)](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff546856(v=vs.85))和[媒体状态指示的 802.11 网络](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff549301(v=vs.85)).

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
<td><p>不受支持 NDIS 6.0 及更高版本 (使用<a href="ndis-status-link-state.md" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](ndis-status-link-state.md)"> <strong>NDIS_STATUS_LINK_STATE</strong> </a>相反)。 仅支持 Windows Vista 和 Windows XP 中的 NDIS 5.1 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_STATUS\_LINK\_STATE**](ndis-status-link-state.md)

[**NDIS\_状态\_媒体\_断开连接**](ndis-status-media-disconnect.md)

 

 




