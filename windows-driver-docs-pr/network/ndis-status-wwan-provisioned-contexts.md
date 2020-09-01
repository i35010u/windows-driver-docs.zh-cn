---
title: NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS
description: 小型端口驱动程序使用 NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS 通知来通知 MB 服务有关预配上下文列表的更新作为网络更新的结果。
ms.assetid: 3ec3d991-98c0-4be3-a157-a04e8565a54b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PROVISIONED_CONTEXTS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d192f70050c03b8db687e0b8a4a81a783aa12834
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210169"
---
# <a name="ndis_status_wwan_provisioned_contexts"></a>NDIS \_ 状态 \_ WWAN \_ 预配 \_ 上下文


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ 预配 \_ 上下文通知来通知 MB 服务有关预配上下文列表作为网络更新的结果的更新。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 预配的 \_ 上下文**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts) 结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须**ElementType**将 NDIS \_ WWAN \_ 预配 \_ 上下文结构**ContextListHeader**的 ElementType 成员设置为**WwanStructContext**。

在某些情况下，已设置上下文的列表由网络通过无线 (OTA) 或短消息服务 (SMS) 进行更新。 微型端口驱动程序必须相应地更新已设置上下文的列表。 此后，小型端口驱动程序必须将此指示用于更新的列表，通知 MB 服务有关更新的信息。

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


[**NDIS \_ WWAN \_ 预配 \_ 上下文**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_provisioned_contexts)

[OID \_ WWAN \_ 预配 \_ 上下文](oid-wwan-provisioned-contexts.md)

 

