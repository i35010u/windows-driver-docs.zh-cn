---
title: WDI_TLV_TCP_OFFLOAD_CAPABILITIES
description: WDI_TLV_TCP_OFFLOAD_CAPABILITIES 是 TLV 包含 TCP/IP 卸载功能。
ms.assetid: 9B3428CC-C9B4-4769-BD97-F25920C4AAF2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TCP_OFFLOAD_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f6b9d322080a76fb0a81011476a177bb9e60b970
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357325"
---
# <a name="wditlvtcpoffloadcapabilities"></a>WDI\_TLV\_TCP\_卸载\_功能


WDI\_TLV\_TCP\_卸载\_功能是包含 TCP/IP 卸载功能 TLV。

将报告功能值，如中所述[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)。 使用 NDIS\_卸载\_不\_支持和 NDIS\_卸载\_时，该值指示通过功能支持[OID\_WDI\_GET\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)。 对于 FIPS 模式下的连接，卸载 OFF 情况下处于状态下，用户设备。

## <a name="tlv-type"></a>TLV 类型


0xCA

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                         |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_CHECKSUM\_卸载\_功能**](wdi-tlv-checksum-offload-capabilities.md)                  |                                |          | 校验和卸载功能。      |
| [**WDI\_TLV\_LSO\_V1\_CAPABILITIES**](wdi-tlv-lso-v1-capabilities.md)                                      |                                |          | 大量发送卸载 V1 功能。 |
| [**WDI\_TLV\_LSO\_V2\_CAPABILITIES**](wdi-tlv-lso-v2-capabilities.md)                                      |                                |          | 大量发送卸载 V2 功能。 |
| [**WDI\_TLV\_RECEIVE\_COALESCE\_OFFLOAD\_CAPABILITIES**](wdi-tlv-receive-coalesce-offload-capabilities.md) |                                |          | 接收卸载功能。       |
| [**WDI_TLV_OFFLOAD_SCOPE**](wdi-tlv-offload-scope.md) |   |   | 指明是否卸载适用于 STA 端口仅或所有端口上。 当前适用于 802.11ad 仅适用于适配器。 |

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

 

 




