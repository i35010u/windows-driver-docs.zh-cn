---
title: NDIS_STATUS_WWAN_SERVICE_ACTIVATION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SERVICE_ACTIVATION 通知来响应 OID_WWAN_SERVICE_ACTIVATION 的 OID 设置请求。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SERVICE_ACTIVATION 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 01c9e5deb80802843c775582f1b69ca7d5928a9e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818851"
---
# <a name="ndis_status_wwan_service_activation"></a>NDIS \_ 状态 \_ WWAN \_ 服务 \_ 激活


微型端口驱动程序使用 NDIS \_ 状态 " \_ wwan \_ 服务 \_ 激活通知" 来响应 oid 设置 [oid \_ WWAN \_ 服务 \_ 激活](oid-wwan-service-activation.md)的请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 NDIS \_ WWAN \_ 服务 \_ 激活 \_ 状态结构。

<a name="remarks"></a>备注
-------

小型端口驱动程序必须返回服务激活状态，以响应 oid [ \_ WWAN \_ 服务 \_ 激活](oid-wwan-service-activation.md)的 oid 设置请求。

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

 

 




