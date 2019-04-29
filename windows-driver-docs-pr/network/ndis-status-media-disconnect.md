---
title: NDIS_STATUS_MEDIA_DISCONNECT
description: NDIS_STATUS_MEDIA_DISCONNECT 状态指示的网络连接的状态已从连接到断开连接。
ms.assetid: 490853ca-c849-4b2b-9639-4be670616101
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_MEDIA_DISCONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 155e63b7bb3d2bf9af0d50f2db842869dc9dc52e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380151"
---
# <a name="ndisstatusmediadisconnect"></a>NDIS\_状态\_媒体\_断开连接


NDIS\_状态\_媒体\_断开连接状态指示的网络连接的状态已更改从已连接到断开连接。 例如，网络设备失去连接，因为它不在范围内 （适用于无线设备） 或用户断开设备的网络电缆。

<a name="remarks"></a>备注
-------

NDIS 转换 NDIS\_状态\_媒体\_到断开连接状态指示[ **NDIS\_状态\_链接\_状态**](ndis-status-link-state.md)状态指示为过量 NDIS 6.0 驱动程序。

NDIS 5。*x*和更早的微型端口驱动程序指示[ **NDIS\_状态\_媒体\_CONNECT** ](ndis-status-media-connect.md)时连接的状态还原。

详细了解 NDIS\_状态\_媒体\_断开连接，请参阅[，该值指示连接状态 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff546856)和[的 802.11 网络媒体状态指示](https://msdn.microsoft.com/library/windows/hardware/ff549301).

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

[**NDIS\_状态\_媒体\_连接**](ndis-status-media-connect.md)

 

 




