---
title: OID_WWAN_DEVICE_SERVICES
description: OID_WWAN_DEVICE_SERVICES 返回微型端口驱动程序支持的设备服务的列表。NDIS_WWAN_DEVICE_SERVICES 结构，它指示受支持的设备服务 Guid。
ms.assetid: 79DB0FC0-9AAA-465D-9479-9AD41BE9F4B4
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SERVICES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bac260ee93b094bb894b90efc76a5899021b0872
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576974"
---
# <a name="oidwwandeviceservices"></a>OID\_WWAN\_DEVICE\_SERVICES


OID\_WWAN\_设备\_服务返回的微型端口驱动程序支持的设备服务的列表。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_到原始请求和更高版本发送 NDIS REQUIRED\_状态\_WWAN\_设备\_服务状态通知包含[ **NDIS\_WWAN\_设备\_服务**](https://msdn.microsoft.com/library/windows/hardware/hh439835)结构，它指示受支持的设备服务 Guid。

不支持组的请求。

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
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




