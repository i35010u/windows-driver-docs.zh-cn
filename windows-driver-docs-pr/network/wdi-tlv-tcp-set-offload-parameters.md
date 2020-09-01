---
title: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS
description: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS 是一种 TLV，其中包含用于 OID_WDI_SET_TCP_OFFLOAD_PARAMETERS 的微型端口适配器的 TCP 卸载功能。
ms.assetid: 1DE1114A-E718-473F-B0EB-92AEFA4E7F13
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 33f1ea687acc8d66f01ea42fd3a22312ce6da01c
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208472"
---
# <a name="wdi_tlv_tcp_set_offload_parameters"></a>WDI \_ TLV \_ TCP \_ 设置 \_ 卸载 \_ 参数


WDI \_ tlv \_ TCP \_ 设置 \_ 卸载 \_ 参数是一个 TLV，其中包含用于 OID 的 tcp 卸载功能 [ \_ WDI \_ 设置 \_ tcp \_ 卸载 \_ 参数](./oid-wdi-set-tcp-offload-parameters.md)。

## <a name="tlv-type"></a>TLV 类型


0xF2

## <a name="length"></a>Length


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
<td>UINT8</td>
<td>微型端口适配器的 IPv4 校验和设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - Disabled.</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 已启用传输并禁用接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 启用接收并禁用传输。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 为传输和接收启用。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP 数据包的 IPv4 校验和设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - Disabled.</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 已启用传输并禁用接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 启用接收并禁用传输。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 为传输和接收启用。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP 数据包的 IPv4 校验和设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - Disabled.</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 已启用传输并禁用接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 启用接收并禁用传输。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 为传输和接收启用。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP 数据包的 IPv6 校验和设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - Disabled.</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 已启用传输并禁用接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 启用接收并禁用传输。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 为传输和接收启用。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP 数据包的 IPv6 校验和设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - Disabled.</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 已启用传输并禁用接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> - 启用接收并禁用传输。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> - 为传输和接收启用。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>大量发送卸载版本 1 (LSOV1) 设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_ENABLED</strong> - LSOV1 已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_DISABLED</strong> - LSOV1 已禁用。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Internet 协议安全 (IPsec) 卸载设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_DISABLED</strong> - IPsec 卸载已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载身份验证标头 (AH) 功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_ESP_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载封装安全有效负载 (ESP) 功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_AND_ESP_ENABLED</strong> - 启用 IPsec 卸载 AH 和 ESP 功能以便进行传输和接收。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 大规模发送卸载版本 2 (LSOV2) 设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 for IPv4 已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - LSOV2 for IPv4 已禁用。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 大规模发送卸载版本 2 (LSOV2) 设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - 已启用 IPv6 的 LSOV2。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - IPv6 的 LSOV2 已禁用。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 连接卸载设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 连接卸载设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指示 IPv4 的接收段合并状态。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC 状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - 已启用 RSC 状态。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - RSC 状态处于禁用状态。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指示 IPv6 的接收段合并状态。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC 状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - 已启用 RSC 状态。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - RSC 状态处于禁用状态。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>该值是标志的按位 "或"。 此设置必须设置为0。 当前未定义任何标志。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Internet 协议安全 (IPsec) 卸载第2版端口，该设置支持 IPv6 和 IPv4。 这会为 IPv6 和 IPv4 支持指定设置。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec 卸载版本2已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2身份验证标头 (AH) 功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2封装安全负载 (ESP) 功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - 启用 IPsec 卸载版本 2 AH 和 ESP 功能，以进行传输和接收。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Internet 协议安全 (IPsec) 卸载支持 IPv4 并不支持 IPv6 的微型端口适配器的版本2设置。 如果微型端口驱动程序支持 IPv6，则 IPsecV2 成员将指定 IPv4 设置，并且不会使用此成员。
<p>有效值是：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec 卸载版本2已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2身份验证标头 (AH) 功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2封装安全负载 (ESP) 功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - 启用 IPsec 卸载版本 2 AH 和 ESP 功能，以进行传输和接收。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>封装的数据包任务卸载。 协议驱动程序将此字段设置为以下值之一。
<p></p>
<ul>
<li><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong> (0) -NVGRE 任务卸载状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_SET_ON</strong> (1) -启用 NVGRE 任务卸载。</li>
<li><strong>NDIS_OFFLOAD_SET_OFF</strong> (2) -禁用 NVGRE 任务卸载。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>封装类型。 仅当封装的数据包任务卸载设置为 <strong>NDIS_OFFLOAD_SET_ON</strong>时，此字段才有效。 如果封装的数据包任务卸载成员未设置为 <strong>NDIS_OFFLOAD_SET_ON</strong>，则此成员为零。 协议驱动程序必须将封装类型设置为对应于其所需封装类型的标志的按位 "或"。 它可以从以下标志中进行选择。
<p></p>
<ul>
<li> (0x00000001) <strong>NDIS_ENCAPSULATION_TYPE_GRE_MAC</strong> (NVGRE) 指定 GRE MAC 封装。</li>
</ul></td>
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


[**NDIS \_ 卸载 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[OID \_ WDI \_ 设置 \_ TCP \_ 卸载 \_ 参数](./oid-wdi-set-tcp-offload-parameters.md)

 

