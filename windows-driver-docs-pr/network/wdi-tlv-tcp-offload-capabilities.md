---
title: WDI_TLV_TCP_OFFLOAD_CAPABILITIES
description: WDI_TLV_TCP_OFFLOAD_CAPABILITIES 是包含 TCP/IP 卸载功能的 TLV。
ms.assetid: 9B3428CC-C9B4-4769-BD97-F25920C4AAF2
ms.date: 07/18/2017
keywords:
- WDI_TLV_TCP_OFFLOAD_CAPABILITIES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a44520bdf680456891f3f71f1a5eb1ddd4e93c2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841725"
---
# <a name="wdi_tlv_tcp_offload_capabilities"></a>WDI\_TLV\_TCP\_卸载\_功能


WDI\_TLV\_TCP\_卸载\_功能是包含 TCP/IP 卸载功能的 TLV。

功能值以[**NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)的形式报告。 使用 NDIS\_卸载\_不\_受支持，并且通过[OID\_WDI\_获取\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)时，支持 NDIS\_卸载\_。 对于采用 FIPS 模式的连接，UE 会关闭卸载。

## <a name="tlv-type"></a>TLV 类型


0xCA

## <a name="length"></a>长度


所有包含的 TLVs 的大小的总和（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                        | 允许多个 TLV 实例 | 可选 | 描述                         |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI\_TLV\_校验和\_卸载\_功能**](wdi-tlv-checksum-offload-capabilities.md)                  |                                |          | 校验和卸载功能。      |
| [**WDI\_TLV\_LSO\_V1\_功能**](wdi-tlv-lso-v1-capabilities.md)                                      |                                |          | 大型发送卸载 V1 功能。 |
| [**WDI\_TLV\_LSO\_V2\_功能**](wdi-tlv-lso-v2-capabilities.md)                                      |                                |          | 大型发送卸载 V2 功能。 |
| [**WDI\_TLV\_接收\_合并\_卸载\_功能**](wdi-tlv-receive-coalesce-offload-capabilities.md) |                                |          | 接收卸载功能。       |
| [**WDI_TLV_OFFLOAD_SCOPE**](wdi-tlv-offload-scope.md) |   |   | 指示是否仅应用于 STA 端口或所有端口。 目前仅适用于 802.11 ad 适配器。 |

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
<td><p>Windows 10</p></td>
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

 

 




