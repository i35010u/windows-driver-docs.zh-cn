---
title: WDI_TLV_CONNECT_PARAMETERS
description: WDI_TLV_CONNECT_PARAMETERS 是包含参数，用于 OID_WDI_TASK_CONNECT 和 OID_WDI_TASK_ROAM TLV。
ms.assetid: 6B2B4E5D-4BF9-4803-A373-FDF64AD3C99B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 276398423da0151c57b16c209e4ada02287717d0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358575"
---
# <a name="wditlvconnectparameters"></a>WDI\_TLV\_CONNECT\_参数


WDI\_TLV\_CONNECT\_参数是包含参数的 TLV [OID\_WDI\_任务\_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-connect)和[OID\_WDI\_任务\_漫游](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-roam)。

## <a name="tlv-type"></a>TLV 类型


0x33

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值

| 在任务栏的搜索框中键入 | 允许多个 TLV 实例 | 可选 | 描述 |
| --- | --- | --- | --- |
| [**WDI\_TLV\_CONNECTION\_SETTINGS**](wdi-tlv-connection-settings.md) |   |   | 连接的设置。 |
| [**WDI\_TLV\_SSID**](wdi-tlv-ssid.md) | X |   | Ssid 允许通过端口连接到的列表。 |
| [**WDI\_TLV\_HESSID**](wdi-tlv-hessid.md) |   | X | 端口允许连接到的 HESSIDs 的列表。 这是一个额外的要求到 SSID 列表。 |
| [**WDI\_TLV\_AUTH\_ALGO\_LIST**](wdi-tlv-auth-algo-list.md) |   |   | 可以使用该连接的身份验证算法的列表。 |
| [**WDI\_TLV\_MULTICAST\_CIPHER\_ALGO\_LIST**](wdi-tlv-multicast-cipher-algo-list.md) |   |   | 可以使用该连接的多路广播的密码算法的列表。 |
| [**WDI\_TLV\_UNICAST\_CIPHER\_ALGO\_LIST**](wdi-tlv-unicast-cipher-algo-list.md) |   |   | 连接可以使用的单播密码算法的列表。 |
| [**WDI\_TLV\_EXTRA\_ASSOCIATION\_REQUEST\_IES**](wdi-tlv-extra-association-request-ies.md) |   | X | 必须包括在发送端口的关联请求 IE blob。 这是适用于任何设备会将与相关联的 BSSID。 除了 BSSID 特定导致浏览器，应使用它。 |
| [**WDI\_TLV\_PHY\_TYPE\_LIST**](wdi-tlv-phy-type-list.md) |   | X | 允许使用的关联的 PHYs 的列表。 如果未指定，则可以使用任何受支持的物理。 如果指定，则设备必须仅使用列出的 PHYs。 |
| [**WDI\_TLV\_DISALLOWED\_BSSIDS\_LIST**](wdi-tlv-disallowed-bssids-list.md) |   | X | 不能用于关联的 BSSIDs 的列表。 如果指定，适配器必须将关联到此列表中任何 AP。 |
| [**WDI\_TLV\_ALLOWED\_BSSIDS\_LIST**](wdi-tlv-allowed-bssids-list.md) |   | X | BSSIDs 允许关联所使用的列表。 如果 WDI 指定 255.255.255.255 则允许所有 BSSIDs。 | 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>
