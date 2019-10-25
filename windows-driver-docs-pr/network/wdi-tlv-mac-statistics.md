---
title: WDI_TLV_MAC_STATISTICS
description: WDI_TLV_MAC_STATISTICS 是一个 TLV，其中包含 OID_WDI_GET_STATISTICS 的每个对等 MAC 统计信息。
ms.assetid: 47ABF170-76D7-4F17-BA92-56E1FEFF729D
ms.date: 07/18/2017
keywords:
- WDI_TLV_MAC_STATISTICS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3b5e873d3fd909d9b1163ebc5eb28fb77f5455c7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826323"
---
# <a name="wdi_tlv_mac_statistics"></a>WDI\_TLV\_MAC\_统计信息


WDI\_TLV\_MAC\_统计信息是一个 TLV，其中包含 OID 的每个对等 MAC 统计信息[\_WDI\_获取\_统计](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-statistics)信息。

## <a name="tlv-type"></a>TLV 类型


0Xa6<

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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>为其设置这些计数的对等方的 MAC 地址。 对于多播和广播数据包，此值设置为 FF-FF-ff-ff-ff-ff。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站的 IEEE MAC 层成功传输的 MSDU 数据包和 MMPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站的 IEEE MAC 层成功接收的 MSDU 数据包和 MMPDU 帧的数量。 对于未通过密码解密或 MIC 验证的接收数据包，此成员不应递增。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>启用 IEEE 802.11 dot11ExcludeUnencrypted 管理信息基础（MIB）对象时，MAC 层丢弃的未加密接收 MPDU 帧的数量。
<p>有关此 MIB 对象的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-exclude-unencrypted" data-raw-source="[OID_DOT11_EXCLUDE_UNENCRYPTED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-exclude-unencrypted)">OID_DOT11_EXCLUDE_UNENCRYPTED</a>。 当 IEEE 802.11 MAC 标头中的 "帧控件" 字段的受保护的帧子字段设置为零时，MPDU 帧被视为未加密。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>由于 MIC 故障，802.11 工作站丢弃的已接收 MSDU 数据包的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>由于 TKIP 重播保护过程，802.11 工作站丢弃的已接收 MPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>由于 TKIP ICV 错误，802.11 工作站未能解密的加密 MPDU 帧的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>由于 AES CCMP 报头格式无效，802.11 丢弃的已接收 MPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>由于 AES CCMP 报头重播保护过程，802.11 工作站丢弃的已接收 MPDU 帧的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站因 AES CCMP 报头解密算法检测到的错误而丢弃的已接收 MPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>收到的 WEP 解密密钥在802.11 工作站上不可用的加密 MPDU 帧的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>由于 WEP ICV 错误，802.11 工作站未能解密的加密 MPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站成功解密的已接收加密数据包的数量。
<p>对于 WEP 和 TKIP 密码算法，端口必须为成功解密的每个已接收加密 MPDU 递增此计数器。 对于 AES-CCMP 报头密码算法，端口必须在已成功解密的每个已收到加密的 MSDU 数据包上增加此计数器的值。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站未能解密的加密数据包的数量。
<p>对于 WEP 和 TKIP 密码算法，端口必须为收到的每个未成功解密的加密 MPDU 递增此计数器。 对于 AES CCMP 报头密码算法，端口必须在收到的每个未成功解密的加密 MSDU 数据包上增加此计数器的值。 此端口不得为成功解密的数据包递增此计数器，但出于其他原因将被丢弃。 例如，由于 TKIP MIC 故障或 TKIP/CCMP 报头重播，端口不得为丢弃的数据包递增此计数器。</p></td>
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

 

 




