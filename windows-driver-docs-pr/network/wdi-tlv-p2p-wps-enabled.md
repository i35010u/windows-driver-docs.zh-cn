---
title: WDI_TLV_P2P_WPS_ENABLED
description: WDI_TLV_P2P_WPS_ENABLED 是一个 TLV，用于指定是否启用 Wi-fi 保护的设置。
ms.assetid: B923DA17-451C-4BF1-8B8B-C2846EDE9774
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_WPS_ENABLED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5863f2a0de0db5161c0aea267a26f8dd7eedf310
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214268"
---
# <a name="wdi_tlv_p2p_wps_enabled"></a>\_已启用 WDI TLV \_ P2P \_ WPS \_


WDI \_ tlv \_ 启用了 tlv \_ \_ ，这是一个 tlv，用于指定是否启用 wi-fi 保护的设置。

## <a name="tlv-type"></a>TLV 类型


0xF7

## <a name="length"></a>Length


UINT8 的大小 (以字节为单位) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>指定是否启用 Wi-fi 保护安装。
<p>有效值为 0 (未启用)  (启用 1) 。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ SET \_ P2P \_ WPS \_ 已启用](./oid-wdi-set-p2p-wps-enabled.md)

 

