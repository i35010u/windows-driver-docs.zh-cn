---
title: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS
description: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS 是一个 TLV，其中包含 OID_WDI_SET_TCP_OFFLOAD_PARAMETERS 的微型端口适配器的 TCP 卸载功能。
ms.assetid: 1DE1114A-E718-473F-B0EB-92AEFA4E7F13
ms.date: 07/18/2017
keywords:
- WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: eafde637f99e6a226fd16f14ef4b6bc548b2e1a5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841729"
---
# <a name="wdi_tlv_tcp_set_offload_parameters"></a>WDI\_TLV\_TCP\_集\_卸载\_参数


WDI\_TLV\_TCP\_集\_卸载\_参数是一个 TLV，其中包含 OID 的微型端口适配器的 TCP 卸载功能[\_WDI\_\_\_\_卸载参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-tcp-offload-parameters)。

## <a name="tlv-type"></a>TLV 类型


0xF2

## <a name="length"></a>长度


所有包含的元素的大小的总和（以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>微型端口适配器的 IPv4 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 允许传输和禁用接收。</li>
<li>为接收和已禁用传输启用<strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -。</li>
<li>为传输和接收启用了<strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP 数据包的 IPv4 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 允许传输和禁用接收。</li>
<li>为接收和已禁用传输启用<strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -。</li>
<li>为传输和接收启用了<strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP 数据包的 IPv4 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 允许传输和禁用接收。</li>
<li>为接收和已禁用传输启用<strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -。</li>
<li>为传输和接收启用了<strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP 数据包的 IPv6 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 允许传输和禁用接收。</li>
<li>为接收和已禁用传输启用<strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -。</li>
<li>为传输和接收启用了<strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP 数据包的 IPv6 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> - 已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> - 允许传输和禁用接收。</li>
<li>为接收和已禁用传输启用<strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -。</li>
<li>为传输和接收启用了<strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>大规模发送卸载版本1（LSOV1）设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_ENABLED</strong> - LSOV1 已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_DISABLED</strong> - LSOV1 处于禁用状态。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Internet 协议安全（IPsec）卸载设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_DISABLED</strong> - IPsec 卸载已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载身份验证标头（AH）功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_ESP_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载封装安全负载（ESP）功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_AND_ESP_ENABLED</strong> - 为传输和接收启用了 IPSEC 卸载 AH 和 ESP 功能。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 大规模发送卸载版本2（LSOV2）设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li>启用 IPv4 的<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2。</li>
<li>已禁用 IPv4 - LSOV2 的<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> 。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 大规模发送卸载版本2（LSOV2）设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li>已启用<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 的 IPv6。</li>
<li>IPv6 的<strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - LSOV2 已禁用。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 连接卸载设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 连接卸载设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指示 IPv4 的接收段合并状态。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC 状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - 已启用 RSC 状态。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - 已禁用 RSC 状态。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指示 IPv6 的接收段合并状态。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC 状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> - 已启用 RSC 状态。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> - 已禁用 RSC 状态。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>该值是标志的按位 "或"。 此设置必须设置为0。 当前未定义任何标志。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Internet 协议安全（IPsec）卸载第2版微型端口适配器，同时支持 IPv6 和 IPv4。 这会为 IPv6 和 IPv4 支持指定设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec 卸载版本2已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2身份验证标头（AH）功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2封装安全负载（ESP）功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - 为传输和接收启用了 IPsec 卸载版本 2 AH 和 ESP 功能。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Internet 协议安全（IPsec）卸载版本2设置，它支持 IPv4 且不支持 IPv6。 如果微型端口驱动程序支持 IPv6，则 IPsecV2 成员将指定 IPv4 设置，并且不会使用此成员。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - 微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> - IPsec 卸载版本2已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2身份验证标头（AH）功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - 应为传输和接收启用 IPsec 卸载版本2封装安全负载（ESP）功能。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - 为传输和接收启用了 IPsec 卸载版本 2 AH 和 ESP 功能。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>封装的数据包任务卸载。 协议驱动程序将此字段设置为以下值之一。
<p></p>
<ul>
<li><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong> （0）-NVGRE 任务卸载状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_SET_ON</strong> （1）-启用 NVGRE 任务卸载。</li>
<li><strong>NDIS_OFFLOAD_SET_OFF</strong> （2）-禁用 NVGRE 任务卸载。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>封装类型。 仅当封装的数据包任务卸载设置为<strong>NDIS_OFFLOAD_SET_ON</strong>时，此字段才有效。 如果封装的数据包任务卸载成员未设置为<strong>NDIS_OFFLOAD_SET_ON</strong>，则此成员为零。 协议驱动程序必须将封装类型设置为对应于其所需封装类型的标志的按位 "或"。 它可以从以下标志中进行选择。
<p></p>
<ul>
<li><strong>NDIS_ENCAPSULATION_TYPE_GRE_MAC</strong> （0x00000001）-指定 GRE MAC 封装（NVGRE）。</li>
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

## <a name="see-also"></a>另请参阅


[**NDIS\_卸载\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload_parameters)

[OID\_WDI\_集\_TCP\_卸载\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-tcp-offload-parameters)

 

 




