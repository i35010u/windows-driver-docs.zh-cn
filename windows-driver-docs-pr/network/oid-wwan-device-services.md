---
title: OID_WWAN_DEVICE_SERVICES
description: OID_WWAN_DEVICE_SERVICES 返回微型端口驱动程序支持的设备服务的列表。NDIS_WWAN_DEVICE_SERVICES 结构，它指示受支持的设备服务 Guid。
ms.assetid: 79DB0FC0-9AAA-465D-9479-9AD41BE9F4B4
ms.date: 08/08/2017
keywords: -OID_WWAN_DEVICE_SERVICES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 790a5a263f760008f75e3ea963e6fdb7af01c0af
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358601"
---
# <a name="oidwwandeviceservices"></a>OID\_WWAN\_DEVICE\_SERVICES


OID\_WWAN\_设备\_服务返回的微型端口驱动程序支持的设备服务的列表。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_到原始请求和更高版本发送 NDIS REQUIRED\_状态\_WWAN\_设备\_服务状态通知包含[ **NDIS\_WWAN\_设备\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)结构，它指示受支持的设备服务 Guid。

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
<td><p>Version</p></td>
<td><p>版本：支持 Windows 8 和更高版本的 Windows 中。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

 

 




