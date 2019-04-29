---
title: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS
description: WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS 是包含 TCP 卸载功能的微型端口适配器 OID_WDI_SET_TCP_OFFLOAD_PARAMETERS TLV。
ms.assetid: 1DE1114A-E718-473F-B0EB-92AEFA4E7F13
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_TCP_SET_OFFLOAD_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: de29cf89066bffa83a00584f91cad64ce3c56901
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366630"
---
# <a name="wditlvtcpsetoffloadparameters"></a>WDI\_TLV\_TCP\_SET\_OFFLOAD\_PARAMETERS


WDI\_TLV\_TCP\_设置\_卸载\_参数是包含 TCP 卸载功能的微型端口适配器的 TLV [OID\_WDI\_集\_TCP\_卸载\_参数](https://msdn.microsoft.com/library/windows/hardware/dn925945)。

## <a name="tlv-type"></a>TLV 类型


0xF2

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

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
<td>IPv4 校验和的微型端口适配器设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -传输和接收的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -接收和传输的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP 数据包 IPv4 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -传输和接收的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -接收和传输的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP 数据包 IPv4 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -传输和接收的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -接收和传输的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>TCP 数据包 IPv6 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -传输和接收的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -接收和传输的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>UDP 数据包 IPv6 校验和设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_DISABLED</strong> -已禁用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_ENABLED_RX_DISABLED</strong> -传输和接收的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RX_ENABLED_TX_DISABLED</strong> -接收和传输的已禁用已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_TX_RX_ENABLED</strong> -启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>大量发送卸载版本 1 (LSOV1) 设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_ENABLED</strong> - LSOV1 已启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV1_DISABLED</strong> - LSOV1 被禁用。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Internet 协议安全性 (IPsec) 卸载设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_DISABLED</strong> -禁用 IPsec 卸载。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_ENABLED</strong> - IPsec 卸载身份验证标头 (AH) 功能可用于传输和接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_ESP_ENABLED</strong> - IPsec 卸载封装安全有效负载 (ESP) 功能可用于传输和接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV1_AH_AND_ESP_ENABLED</strong> - IPsec 卸载 AH 和 ESP 功能启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 大量发送卸载版本 2 (LSOV2) 设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 IPv4 为启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> - ipv4 LSOV2 被禁用。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 大量发送卸载版本 2 (LSOV2) 设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_ENABLED</strong> - LSOV2 IPv6 的启用。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_LSOV2_DISABLED</strong> -禁用 IPv6 的 LSOV2。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>IPv4 连接卸载设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>IPv6 连接卸载设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>对 IPv4 指示接收段合并状态。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC 状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> -启用 RSC 状态。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> -禁用 RSC 状态。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指示 IPv6 接收段合并状态。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> - RSC 状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_ENABLED</strong> -启用 RSC 状态。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_RSC_DISABLED</strong> -禁用 RSC 状态。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>值是标志的按位 OR。 这必须设置为 0。 没有当前定义的标志。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Internet 协议安全性 (IPsec) 将卸载版本 2 支持 IPv6 和 IPv4 的微型端口适配器设置。 这将指定的 IPv6 和 IPv4 支持的设置。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> -禁用 IPsec 卸载版本 2。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - IPsec 卸载版本 2 身份验证标头 (AH) 功能可用于传输和接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - IPsec 卸载版本 2 封装安全有效负载 (ESP) 功能可用于传输和接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - IPsec 卸载版本 2 AH 和 ESP 功能启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Internet 协议安全性 (IPsec) 将卸载版本 2 支持 IPv4，而且不支持 IPv6 的微型端口适配器的设置。 如果微型端口驱动程序支持 IPv6，IPsecV2 成员指定不使用 IPv4 设置和此成员。
<p>有效值包括：</p>
<ul>
<li><strong>NDIS_OFFLOAD_PARAMETERS_NO_CHANGE</strong> -微型端口驱动程序不应更改当前设置。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_DISABLED</strong> -禁用 IPsec 卸载版本 2。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_ENABLED</strong> - IPsec 卸载版本 2 身份验证标头 (AH) 功能可用于传输和接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_ESP_ENABLED</strong> - IPsec 卸载版本 2 封装安全有效负载 (ESP) 功能可用于传输和接收。</li>
<li><strong>NDIS_OFFLOAD_PARAMETERS_IPSECV2_AH_AND_ESP_ENABLED</strong> - IPsec 卸载版本 2 AH 和 ESP 功能启用了传输和接收。</li>
</ul></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>封装数据包任务卸载。 协议驱动程序将此字段设置为以下值之一。
<p></p>
<ul>
<li><strong>NDIS_OFFLOAD_SET_NO_CHANGE</strong> (0)-NVGRE 任务卸载状态保持不变。</li>
<li><strong>NDIS_OFFLOAD_SET_ON</strong> (1)-启用 NVGRE 任务卸载。</li>
<li><strong>NDIS_OFFLOAD_SET_OFF</strong> (2)-禁用 NVGRE 任务卸载。</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>封装类型。 仅当封装数据包任务卸载设置时，此字段才有效<strong>NDIS_OFFLOAD_SET_ON</strong>。 如果封装数据包任务卸载成员未设置为<strong>NDIS_OFFLOAD_SET_ON</strong>，此成员为零。 协议驱动程序必须设置封装类型的按位或的对应于它需要的封装类型的标志。 它可以选择从以下标志。
<p></p>
<ul>
<li><strong>NDIS_ENCAPSULATION_TYPE_GRE_MAC</strong> (0x00000001)-指定 GRE MAC 封装 (NVGRE)。</li>
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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_卸载\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566706)

[OID\_WDI\_SET\_TCP\_OFFLOAD\_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/dn925945)

 

 




