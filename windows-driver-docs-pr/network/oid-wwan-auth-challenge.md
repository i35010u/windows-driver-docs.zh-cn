---
title: OID_WWAN_AUTH_CHALLENGE
description: OID_WWAN_AUTH_CHALLENGE 将身份验证质询发送到订阅服务器上标识模块 (SIM) 卡，以从包含 NDIS_WWAN_ SIM.n NDIS_STATUS_WWAN_AUTHENTICATION_RESPONSE 状态通知获取响应的 MB 设备完成查询请求时，AUTHENTICATION_RESPONSE 结构来提供身份验证密钥请求由调用方根据的挑战。
ms.assetid: C39300F2-DF14-4DA8-9BD2-83593CC29837
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_AUTH_CHALLENGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d760f90c006b80835d53ad4f52ebac535448e840
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372865"
---
# <a name="oidwwanauthchallenge"></a>OID\_WWAN\_身份验证\_质询


OID\_WWAN\_身份验证\_挑战将身份验证质询发送到订阅服务器上标识模块 (SIM) 卡，以从 SIM 获取响应的 MB 设备。

不支持组的请求。

这是可选的 OID。 当微型端口驱动程序实现它时，它们必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_必需到原始请求和更高版本发送 NDIS\_状态\_WWAN\_身份验证\_响应状态通知，其中包含 NDIS\_WWAN\_身份验证\_响应结构来提供身份验证密钥完成查询请求时，所请求由调用方根据的挑战。

<a name="remarks"></a>备注
-------

在处理此 OID 时，微型端口驱动程序可以访问 SIM 卡，但不是应访问提供程序网络。 此 OID 必须甚至在单选关闭或飞行模式工作。

OID\_WWAN\_身份验证\_质询支持第二代和第三代移动网络。 SIM 指定基于 GSM 身份验证和密钥协议基元，这是标准的第二代移动网络的身份验证机制。 也称为和也称为使用第三代身份验证和密钥协议机制，指定为通用移动通信系统 (UMTS) 中\[TS33.102\]以及在 CDMA2000 \[S.S0055 A\]具体取决于设备的功能。

微型端口驱动程序应返回 NDIS\_状态\_不\_支持如果它们不支持返回一个或所有身份验证方法。

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
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




