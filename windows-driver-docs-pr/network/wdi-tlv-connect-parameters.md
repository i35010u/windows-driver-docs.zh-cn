---
title: WDI_TLV_CONNECT_PARAMETERS
description: WDI_TLV_CONNECT_PARAMETERS 是包含 OID_WDI_TASK_CONNECT 和 OID_WDI_TASK_ROAM 参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CONNECT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4ad8b3dbb52e62ae0ffcee8299d5d6d27db49291
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822741"
---
# <a name="wdi_tlv_connect_parameters"></a>WDI \_ TLV \_ 连接 \_ 参数


WDI \_ tlv \_ 连接 \_ 参数是一个 tlv，其中包含用于 [oid \_ WDI \_ task \_ CONNECT](./oid-wdi-task-connect.md) 和 [oid \_ WDI \_ 任务 \_ 漫游](./oid-wdi-task-roam.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0x33

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值

| 类型 | 允许多个 TLV 实例 | 可选 | 说明 |
| --- | --- | --- | --- |
| [**WDI \_ TLV \_ 连接 \_ 设置**](wdi-tlv-connection-settings.md) |   |   | 连接的设置。 |
| [**WDI \_ TLV \_ SSID**](wdi-tlv-ssid.md) | X |   | 允许该端口连接到的 Ssid 列表。 |
| [**WDI \_ TLV \_ HESSID**](wdi-tlv-hessid.md) |   | X | 允许端口连接到的 HESSIDs 的列表。 这是对 SSID 列表的附加要求。 |
| [**WDI \_ TLV \_ 身份验证 \_ 算法 \_ 列表**](wdi-tlv-auth-algo-list.md) |   |   | 连接可使用的身份验证算法的列表。 |
| [**WDI \_ TLV \_ 多播 \_ 密码 \_ 算法 \_ 列表**](wdi-tlv-multicast-cipher-algo-list.md) |   |   | 连接可以使用的多播密码算法的列表。 |
| [**WDI \_ TLV \_ 单播 \_ 密码 \_ 算法 \_ 列表**](wdi-tlv-unicast-cipher-algo-list.md) |   |   | 连接可以使用的单播密码算法的列表。 |
| [**WDI \_ TLV \_ 额外 \_ 关联 \_ 请求 \_**](wdi-tlv-extra-association-request-ies.md) |   | X | 必须包含在端口发送的关联请求中的 IE blob。 这适用于设备将关联的所有 BSSID。 除了特定的 BSSID 外，还应使用此方法。 |
| [**WDI \_ TLV \_ PHY \_ 类型 \_ 列表**](wdi-tlv-phy-type-list.md) |   | X | 允许用于关联的 PHYs 的列表。 如果未指定，则可使用任何受支持的 PHY。 如果指定，设备必须仅使用所列的 PHYs。 |
| [**WDI \_ TLV 不 \_ 允许 \_ BSSIDS \_ 列表**](wdi-tlv-disallowed-bssids-list.md) |   | X | 不允许用于关联的 BSSIDs 的列表。 如果已指定，则适配器不得关联到此列表中的任何 AP。 |
| [**WDI \_ TLV \_ 允许 \_ BSSIDS \_ 列表**](wdi-tlv-allowed-bssids-list.md) |   | X | 允许用于关联的 BSSIDs 的列表。 如果 WDI 指定255.255.255.255，则允许使用所有 BSSIDs。 | 

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
