---
title: NDIS_STATUS_WWAN_MODEM_CONFIG_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_MODEM_CONFIG_INFO 通知来告知 MB 服务关于完成的上一个 OID_WWAN_MODEM_CONFIG_INFO 查询请求。
ms.assetid: 9D56BCE1-2CCF-4BD0-A646-4510642EB08A
keywords:
- NDIS_STATUS_WWAN_MODEM_CONFIG_INFO，与 Windows Vista 一起启动的网络驱动程序
topic_type:
- apiref
api_name:
- NDIS_STATUS_WWAN_MODEM_CONFIG_INFO
api_location:
- ndis.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9763e582e0470c8f40eb09d7d4401052cf351158
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524784"
---
# <a name="ndisstatuswwanmodemconfiginfo"></a>NDIS_STATUS_WWAN_MODEM_CONFIG_INFO


MBB 驱动程序使用**NDIS_STATUS_WWAN_MODEM_CONFIG_INFO**通知来通知 MB 服务关于完成的上一次[OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md)查询请求。

MBB 驱动程序必须仅发送未经请求**NDIS_STATUS_WWAN_MODEM_CONFIG_INFO**调制解调器的配置状态已更改。

使用此通知[ **NDIS_WWAN_MODEM_CONFIG_INFO** ](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)结构。

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
<td><p>Windows 10 版本 1709</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID_WWAN_MODEM_CONFIG_INFO](oid-wwan-modem-config-info.md)

[**NDIS_WWAN_MODEM_CONFIG_INFO**](https://msdn.microsoft.com/library/windows/hardware/07C2BAED-157A-459C-B558-115C0091ECE5)
 

