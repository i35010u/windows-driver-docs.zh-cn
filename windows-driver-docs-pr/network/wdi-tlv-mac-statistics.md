---
title: WDI_TLV_MAC_STATISTICS
description: WDI_TLV_MAC_STATISTICS 是包含 OID_WDI_GET_STATISTICS 的每对等 MAC 统计信息的 TLV。
ms.assetid: 47ABF170-76D7-4F17-BA92-56E1FEFF729D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_MAC_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6af95c0c583bc8d38c3fe9d0a8c301a70d2ae5d7
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104766"
---
# <a name="wdi_tlv_mac_statistics"></a>WDI \_ TLV \_ MAC \_ 统计信息


WDI \_ tlv \_ mac \_ 统计信息是一个 tlv，其中包含 [OID \_ WDI \_ 获取 \_ 统计](./oid-wdi-get-statistics.md)信息的每个对等 MAC 统计信息。

## <a name="tlv-type"></a>TLV 类型


0Xa6<

## <a name="length"></a>长度


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
<td><a href="/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)"><strong>WDI_MAC_ADDRESS</strong></a></td>
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
<td>启用 IEEE 802.11 dot11ExcludeUnencrypted 管理信息基础 (MIB) 对象时，MAC 层丢弃的未加密接收 MPDU 帧的数量。
<p>有关此 MIB 对象的详细信息，请参阅 <a href="/windows-hardware/drivers/network/oid-dot11-exclude-unencrypted" data-raw-source="[OID_DOT11_EXCLUDE_UNENCRYPTED](/previous-versions/windows/hardware/wireless/oid-dot11-exclude-unencrypted)">OID_DOT11_EXCLUDE_UNENCRYPTED</a>。 当 IEEE 802.11 MAC 标头中的 "帧控件" 字段的受保护的帧子字段设置为零时，MPDU 帧被视为未加密。</p></td>
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

