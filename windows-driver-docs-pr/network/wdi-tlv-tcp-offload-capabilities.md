---
title: WDI_TLV_TCP_OFFLOAD_CAPABILITIES
description: WDI_TLV_TCP_OFFLOAD_CAPABILITIES 是包含 TCP/IP 卸载功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TCP_OFFLOAD_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f187e0c704070e1cb7dab2a8bf56e1dd2e8cf823
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834139"
---
# <a name="wdi_tlv_tcp_offload_capabilities"></a>WDI \_ TLV \_ TCP \_ 卸载 \_ 功能


WDI \_ tlv \_ tcp \_ 卸载 \_ 功能是包含 TCP/IP 卸载功能的 tlv。

将按 [**NDIS \_ TCP \_ IP \_ 校验和 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)中所述报告功能值。 使用 \_ \_ 不 \_ 受支持的 ndis 卸载，并 \_ \_ 在通过 [OID \_ WDI \_ 获取 \_ 适配器 \_ 功能](./oid-wdi-get-adapter-capabilities.md)指示功能时支持 ndis 卸载。 对于采用 FIPS 模式的连接，UE 会关闭卸载。

## <a name="tlv-type"></a>TLV 类型


0xCA

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                        | 允许多个 TLV 实例 | 可选 | 说明                         |
|-------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------|
| [**WDI \_ TLV \_ 校验和 \_ 卸载 \_ 功能**](wdi-tlv-checksum-offload-capabilities.md)                  |                                |          | 校验和卸载功能。      |
| [**WDI \_ TLV \_ LSO \_ V1 \_ 功能**](wdi-tlv-lso-v1-capabilities.md)                                      |                                |          | 大型发送卸载 V1 功能。 |
| [**WDI \_ TLV \_ LSO \_ V2 \_ 功能**](wdi-tlv-lso-v2-capabilities.md)                                      |                                |          | 大型发送卸载 V2 功能。 |
| [**WDI \_ TLV \_ 接收 \_ 联合 \_ 卸载 \_ 功能**](wdi-tlv-receive-coalesce-offload-capabilities.md) |                                |          | 接收卸载功能。       |
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

 

