---
title: WDI_TLV_CHECKSUM_OFFLOAD_V4_TX_PARAMETERS (0xD1)
description: WDI_TLV_CHECKSUM_OFFLOAD_V4_TX_PARAMETERS 是包含参数的 IPv4 Tx 校验和卸载 TLV。
ms.assetid: EA862CDA-5FF4-4C5F-A522-224714640F34
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_CHECKSUM_OFFLOAD_V4_TX_PARAMETERS (0xD1) 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3e9576bdaeb4e767e4c62f4bb070a67ab8923044
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387198"
---
# <a name="wditlvchecksumoffloadv4txparameters-0xd1"></a>WDI\_TLV\_CHECKSUM\_卸载\_V4\_TX\_参数 (0xD1)


WDI\_TLV\_CHECKSUM\_卸载\_V4\_TX\_参数是包含参数的 IPv4 Tx 校验和卸载 TLV。

将报告功能值，如中所述[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_ip_checksum_offload)。 使用 NDIS\_卸载\_不\_支持和 NDIS\_卸载\_时，该值指示通过功能支持[OID\_WDI\_GET\_适配器\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)。

## <a name="tlv-type"></a>TLV 类型


0xD1

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
<td>UINT32</td>
<td>封装的设置。 有效值包括：
<ul>
<li>WDI_ENCAPSULATION_IEEE_802_11</li>
</ul></td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定是否支持使用 IP 选项的校验和卸载。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定是否支持使用 TCP 选项的校验和卸载。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定是否启用了 TCP 校验和卸载。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定是否启用 UDP 卸载。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定是否启用了 IP 校验和。</td>
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

 

 




