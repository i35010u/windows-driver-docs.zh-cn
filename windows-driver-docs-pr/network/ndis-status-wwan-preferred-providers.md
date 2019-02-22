---
title: NDIS_STATUS_WWAN_PREFERRED_PROVIDERS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 通知来告知首选提供程序列表 (PPL) 已更改 MB 服务。
ms.assetid: b0c06db9-82ca-4f94-80e6-3cf13197abf5
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 089a08a8b4de53142a90d5b4e5992bbbe7f26fa7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555319"
---
# <a name="ndisstatuswwanpreferredproviders"></a>NDIS\_状态\_WWAN\_首选\_提供程序


微型端口驱动程序使用 NDIS\_状态\_WWAN\_首选\_提供程序通知来通知首选提供程序列表 (PPL) 已更改 MB 服务。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_首选\_提供程序**](https://msdn.microsoft.com/library/windows/hardware/ff567913)结构。

<a name="remarks"></a>备注
-------

在某些情况下，PPL （适用于基于 GSM 的设备） 更新的网络是无线 (OTA) 或短消息服务 (SMS)。 微型端口驱动程序必须相应地更新 PPL。 此后，微型端口驱动程序必须通知有关与更新 PPL 使用这种指示更新 MB 服务。 为基于 GSM 的网络**PreferredListHeader**成员的 NDIS\_WWAN\_首选\_提供程序结构必须指向已更新 PPL。

微型端口驱动程序使用这种指示通知 MB 服务有关的更新[OID\_WWAN\_PREFERRED\_提供程序](oid-wwan-preferred-providers.md) MB 服务中的集请求。 对 OID 的响应\_WWAN\_PREFERRED\_提供程序集请求必须包含在零个元素**PreferredListHeader**成员。

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_PREFERRED\_PROVIDERS**](https://msdn.microsoft.com/library/windows/hardware/ff567913)

[OID\_WWAN\_PREFERRED\_PROVIDERS](oid-wwan-preferred-providers.md)

 

 




