---
title: WDI_TLV_MAC_STATISTICS
description: WDI_TLV_MAC_STATISTICS 是 TLV OID_WDI_GET_STATISTICS 包含每个对等的 MAC 统计数据。
ms.assetid: 47ABF170-76D7-4F17-BA92-56E1FEFF729D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_MAC_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 481a205b151feb4d9993db3f56fb419b2bc1c4f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377003"
---
# <a name="wditlvmacstatistics"></a>WDI\_TLV\_MAC\_STATISTICS


WDI\_TLV\_MAC\_统计信息是包含每个对等的 MAC 统计信息 TLV [OID\_WDI\_获取\_统计信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-statistics)。

## <a name="tlv-type"></a>TLV 类型


0xA6

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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address" data-raw-source="[&lt;strong&gt;WDI_MAC_ADDRESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)"><strong>WDI_MAC_ADDRESS</strong></a></td>
<td>为设置这些计数的对等方的 MAC 地址。 对于多播和广播数据包，此值设置为 FF-FF-FF-FF-FF-FF-FF。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU 数据包和 MMPDU IEEE MAC 层的 802.11 工作站成功传输的帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MSDU 数据包和 MMPDU IEEE MAC 层的 802.11 工作站成功接收的帧数。 不应为接收到密码解密或 MIC 验证失败的数据包会增加此成员。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>未加密 MAC 层，当启用 IEEE 802.11 dot11ExcludeUnencrypted 管理信息基础 (MIB) 对象时放弃的收到 MPDU 帧数。
<p>有关此 MIB 对象的详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-exclude-unencrypted" data-raw-source="[OID_DOT11_EXCLUDE_UNENCRYPTED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-dot11-exclude-unencrypted)">OID_DOT11_EXCLUDE_UNENCRYPTED</a>。 MPDU 帧被视为未加密的 IEEE 802.11 MAC 报头中的帧控制字段受保护的框架子字段设置为零。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>接收到 MSDU 丢弃的数据包 802.11 工作站因为 MIC 故障数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>接收到 802.11 工作站因 TKIP 重播保护过程而丢弃的 MPDU 帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>无法解密由于 TKIP ICV 错误 802.11 工作站的加密 MPDU 帧数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>接收到 802.11 因无效的 AES CCMP 格式而丢弃的 MPDU 帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>接收到 802.11 工作站因 AES CCMP 重播保护过程而丢弃的 MPDU 帧数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>接收到 802.11 工作站因 AES CCMP 解密算法检测到的错误而丢弃的 MPDU 帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>加密 MPDU 接收的帧数为其 WEP 解密密钥不可用的 802.11 工作站。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>无法解密由于 WEP ICV 错误 802.11 工作站的加密 MPDU 帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>接收到 802.11 工作站成功解密的加密数据包数。
<p>WEP 和 TKIP 加密算法，该端口必须为每个已成功解密的接收加密 MPDU 递增此计数器。 AES CCMP 的密码算法，该端口必须递增此计数器在每个接收加密 MSDU 数据包已成功解密。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站无法解密的加密数据包数。
<p>WEP 和 TKIP 加密算法，该端口必须为每个接收的加密 MPDU 不成功解密的递增此计数器。 AES CCMP 的密码算法，该端口必须递增此计数器不成功解密每个接收加密 MSDU 数据包上。 端口必须递增此计数器解密的成功，但由于其他原因而被丢弃的数据包。 例如，该端口必须递增此计数器为因 TKIP MIC 故障而丢弃的数据包或 TKIP/CCMP 重播。</p></td>
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

 

 




