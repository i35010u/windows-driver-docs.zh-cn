---
title: NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS 通知来告知 MB 服务有关的预配的上下文，由于网络更新列表的更新。
ms.assetid: 3ec3d991-98c0-4be3-a157-a04e8565a54b
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 44590017fcb49bb1b7d14f9937555c8e88c13f36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377590"
---
# <a name="ndisstatuswwanprovisionedcontexts"></a>NDIS\_状态\_WWAN\_已设置\_上下文


微型端口驱动程序使用 NDIS\_状态\_WWAN\_已设置\_上下文通知来通知 MB 服务有关的预配的上下文，由于网络更新列表的更新。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_已预配\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须设置**ElementType**成员的 NDIS\_WWAN\_已预配\_上下文结构**ContextListHeader**到**WwanStructContext**。

在某些情况下，预配的上下文的列表更新的网络是无线 (OTA) 或短消息服务 (SMS)。 微型端口驱动程序必须相应地更新预配的上下文的列表。 此后，微型端口驱动程序必须通知有关此指示使用的更新列表的更新 MB 服务。

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_已设置\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)

[OID\_WWAN\_已设置\_上下文](oid-wwan-provisioned-contexts.md)

 

 




