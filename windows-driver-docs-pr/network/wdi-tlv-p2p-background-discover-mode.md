---
title: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE
description: WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE 是包含 Wi-fi Direct 后台发现模式参数的 TLV。
ms.assetid: 987DB282-A992-497F-98B5-0D3DD477B91C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_BACKGROUND_DISCOVER_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4a0af619f02151e351ee600f20bb37f25f97db0b
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90105660"
---
# <a name="wdi_tlv_p2p_background_discover_mode"></a>WDI \_ TLV \_ P2P \_ 后台 \_ 发现 \_ 模式


WDI \_ tlv \_ P2P \_ 后台 \_ 发现 \_ 模式是包含 wi-fi Direct 后台发现模式参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xCE

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

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
<td><a href="/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_discover_type" data-raw-source="[&lt;strong&gt;WDI_P2P_DISCOVER_TYPE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_discover_type)"><strong>WDI_P2P_DISCOVER_TYPE</strong></a></td>
<td>端口要执行的发现的类型。</td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></td>
<td>端口要执行的服务发现的类型。
<p>唯一有效的值是 WDI_P2P_SERVICE_DISCOVERY_TYPE_NO_SERVICE_DISCOVERY 和 WDI_P2P_SERVICE_DISCOVERY_TYPE_SERVICE_NAME_ONLY。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>设备可见性超时。 指定用于报告设备条目的最大超时 (以毫秒为单位) 。 这对于后台扫描是必需的。</td>
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

