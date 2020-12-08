---
title: WDI_TLV_P2P_WPS_ENABLED
description: WDI_TLV_P2P_WPS_ENABLED 是一个 TLV，用于指定是否启用 Wi-Fi 受保护的设置。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_WPS_ENABLED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b58b52e351956f31a6865cb55754b8e515961f01
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818119"
---
# <a name="wdi_tlv_p2p_wps_enabled"></a>\_已启用 WDI TLV \_ P2P \_ WPS \_


\_已启用 WDI tlv 的 tlv \_ \_ \_ 是一个 tlv，用于指定是否启用 Wi-Fi 受保护的设置。

## <a name="tlv-type"></a>TLV 类型


0xF7

## <a name="length"></a>长度


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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>指定是否启用 Wi-Fi 受保护的设置。
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ SET \_ P2P \_ WPS \_ 已启用](./oid-wdi-set-p2p-wps-enabled.md)

 

