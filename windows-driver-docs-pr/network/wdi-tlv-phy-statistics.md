---
title: WDI_TLV_PHY_STATISTICS
description: WDI_TLV_PHY_STATISTICS 是包含每个物理统计信息的 OID_WDI_GET_STATISTICS TLV。
ms.assetid: 2F27FF4E-54AC-4518-AEB0-3518FBC8BE0F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PHY_STATISTICS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71fe7efbc022fef9047a97f7bb2bd7bc54a6d089
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392872"
---
# <a name="wditlvphystatistics"></a>WDI\_TLV\_PHY\_统计信息


WDI\_TLV\_PHY\_统计信息是包含每个物理统计信息的 TLV [OID\_WDI\_获取\_统计信息](https://msdn.microsoft.com/library/windows/hardware/dn925850)。

## <a name="tlv-type"></a>TLV 类型


0xA7

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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926105" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926105)"><strong>WDI_PHY_TYPE</strong></a></td>
<td>此 PHY 的类型。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU 数据包和 MMPDU IEEE 物理层的 802.11 工作站已成功传输的帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>多播或广播 MSDU 数据包和 MMPDU IEEE 物理层的 802.11 工作站已成功传输的帧数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU 数据包和 802.11 工作站未能传输超出 802.11 IEEE dot11ShortRetryLimit 或 dot11LongRetryLimit MIB 计数器定义的重试限制后的 MMPDU 帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>一个或多个尝试后成功传输 802.11 工作站 MSDU 数据包和 MMPDU 帧数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站后超过一次重新传输尝试成功传输的 MSDU 数据包和 MMPDU 帧数。
<p>对于 MSDU 的数据包，该端口必须递增每个包已成功传输一个或多个其 MPDU 所需的片段重新传输后，此计数器。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>MSDU 数据包和 MMPDU 802.11 工作站由 IEEE 802.11 dot11MaxTransmitMSDULifetime MIB 对象定义传输因超时而失败的帧数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站传输和接收的 802.11 ACK 帧通过确认 MPDU 帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站到请求发送 (RTS) 框架的响应中收到清除发送 (CTS) 帧次数。 如果这不会保持每个端口，它可以维护每个通道。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站未收到响应 RTS 帧 CTS 帧次数。 如果这不会保持每个端口，它可以维护每个通道。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>次数 802.11 工作站预期和未收到确认 (ACK) 框架。 如果这不会保持每个端口，它可以维护每个通道。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU 数据包和 MMPDU 802.11 工作站已成功接收的帧数。
<p>对于 MSDU 的数据包，该端口必须递增每个数据包的 MPDU 片段已收到而传递帧检查顺序 (FCS) 验证和重放检测此计数器。 端口必须递增此成员，无论是否接收 MSDU 数据包或 MPDU 片段失败 MAC 层密码解密。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>多播或广播 MSDU 数据包和 MMPDU 802.11 工作站已成功接收的帧数。
<p>对于 MSDU 的数据包，端口必须递增此计数器每个数据包，其 MPDU 片段已收到而传递 FCS 验证和重放检测。 端口必须递增此成员，无论是否接收 MSDU 数据包或 MPDU 片段失败 MAC 层密码解密。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>MSDU 数据包或启用混杂数据包筛选器时，收到的 802.11 工作站 MMPDU 帧数。 如果这不会保持每个端口，它可以维护每个通道。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>如果 MSDU 数据包和 MMPDU 帧的 802.11 站放弃由于定义的 IEEE 802.11 dot11MaxReceiveLifetime 超时 MIB 对象的数目。 如果这不会保持每个端口，它可以维护每个通道。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 无线站接收到的重复 MPDU 帧数。 802.11 工作站确定通过 802.11 MAC 报头的序列控制字段重复帧。 如果这不会保持每个端口，它可以维护每个通道。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>收到的 802.11 工作站进行 MSDU 数据包或 MMPDU 帧 MPDU 帧数。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>已启用混杂数据包筛选器时，收到的 802.11 工作站进行 MSDU 数据包或 MMPDU 帧 MPDU 帧数。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站收到带有 FCS 错误的 MPDU 帧数。 如果这不会保持每个端口，它可以维护每个通道。</td>
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

 

 




