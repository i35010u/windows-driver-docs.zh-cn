---
title: NDIS_STATUS_WWAN_SERVICE_ACTIVATION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SERVICE_ACTIVATION 通知来响应的 OID_WWAN_SERVICE_ACTIVATION OID 集请求。
ms.assetid: c5700759-b903-4564-a8b8-c49140d2acd3
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SERVICE_ACTIVATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9429f62e9c7d16de1f983d603e105e4c603786f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379300"
---
# <a name="ndisstatuswwanserviceactivation"></a>NDIS\_状态\_WWAN\_服务\_激活


微型端口驱动程序使用 NDIS\_状态\_WWAN\_服务\_激活通知 OID 响应设置的请求[OID\_WWAN\_服务\_激活](oid-wwan-service-activation.md)。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

此通知使用 NDIS\_WWAN\_服务\_激活\_状态结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须在 OID 集请求的响应中返回的服务激活状态[OID\_WWAN\_服务\_激活](oid-wwan-service-activation.md)。

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

 

 




