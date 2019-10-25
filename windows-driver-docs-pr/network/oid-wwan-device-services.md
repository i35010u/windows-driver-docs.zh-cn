---
title: OID_WWAN_DEVICE_SERVICES
description: OID_WWAN_DEVICE_SERVICES 返回微型端口驱动程序所支持的设备服务的列表。NDIS_WWAN_DEVICE_SERVICES 结构，指示支持的设备服务 Guid。
ms.assetid: 79DB0FC0-9AAA-465D-9479-9AD41BE9F4B4
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 37f4ed3b522775ba7333fb713bfcd944d64869fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843850"
---
# <a name="oid_wwan_device_services"></a>OID\_WWAN\_设备\_服务


OID\_WWAN\_设备\_服务返回微型端口驱动程序所支持的设备服务列表。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，稍后将 NDIS\_状态\_WWAN\_设备发送\_服务状态通知，其中包含一个[**NDIS\_WWAN\_设备\_服务**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)结构，该结构指示受支持的设备服务 guid。

不支持设置请求。

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
<td><p>版本：在 windows 8 及更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

 

 




