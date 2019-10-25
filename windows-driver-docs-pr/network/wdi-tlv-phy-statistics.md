---
title: WDI_TLV_PHY_STATISTICS
description: WDI_TLV_PHY_STATISTICS 是一个 TLV，其中包含 OID_WDI_GET_STATISTICS 的每个 PHY 统计信息。
ms.assetid: 2F27FF4E-54AC-4518-AEB0-3518FBC8BE0F
ms.date: 07/18/2017
keywords:
- WDI_TLV_PHY_STATISTICS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e2fb5ee4f611ca6f0a9c0a8863ce4edf23d74902
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844807"
---
# <a name="wdi_tlv_phy_statistics"></a>WDI\_TLV\_PHY\_统计信息


WDI\_TLV\_PHY\_统计信息是一个 TLV，其中包含 OID 的每个 PHY 统计信息[\_WDI\_获取\_统计信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-statistics)。

## <a name="tlv-type"></a>TLV 类型


0xA7

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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)"><strong>WDI_PHY_TYPE</strong></a></td>
<td>此 PHY 的类型。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站的 IEEE PHY 层已成功传输的 MSDU 数据包和 MMPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站的 IEEE PHY 层已成功传输的多播或广播 MSDU 数据包和 MMPDU 帧的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>超过 802.11 IEEE dot11ShortRetryLimit 或 dot11LongRetryLimit MIB 计数器定义的重试限制后802.11 工作站未能传输的 MSDU 数据包和 MMPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>一次或多次尝试后802.11 工作站成功传输的 MSDU 数据包和 MMPDU 帧的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>在多次重新传输尝试后802.11 工作站成功传输的 MSDU 数据包和 MMPDU 帧的数量。
<p>对于 MSDU 数据包，端口必须为每个已成功传输的数据包递增此计数器。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>由于 IEEE 802.11 dot11MaxTransmitMSDULifetime MIB 对象定义的超时，802.11 站无法传输的 MSDU 数据包和 MMPDU 帧的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站通过收到的 802.11 ACK 帧传输和确认的 MPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站收到响应发送（RTS）帧的明文发送（CTS）帧的次数。 如果每个端口无法维护此情况，则可以按通道进行维护。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站为响应 RTS 帧而未接收到 CTS 帧的次数。 如果每个端口无法维护此情况，则可以按通道进行维护。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站预期和未收到确认（ACK）帧的次数。 如果每个端口无法维护此情况，则可以按通道进行维护。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站成功接收的 MSDU 数据包和 MMPDU 帧的数量。
<p>对于 MSDU 数据包，端口必须为收到 MPDU 片段并通过帧检查序列（FCS）验证和重播检测的每个数据包递增此计数器。 无论接收到的 MSDU 数据包或 MPDU 片段是否无法通过 MAC 层密码解密，端口都必须递增此成员。</p></td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站成功接收的多播或广播 MSDU 数据包和 MMPDU 帧的数量。
<p>对于 MSDU 数据包，端口必须为每个数据包递增此计数器，每个数据包都接收了 MPDU 片段，并通过了 FCS 验证和重播检测。 无论接收到的 MSDU 数据包或 MPDU 片段是否无法通过 MAC 层密码解密，端口都必须递增此成员。</p></td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>启用混杂数据包筛选器时，802.11 工作站收到的 MSDU 数据包或 MMPDU 帧的数量。 如果每个端口无法维护此情况，则可以按通道进行维护。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>由于 IEEE 802.11 dot11MaxReceiveLifetime MIB 对象定义的超时而导致802.11 工作站丢弃的 MSDU 数据包和 MMPDU 帧的数目。 如果每个端口无法维护此情况，则可以按通道进行维护。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>802.11 工作站收到的重复 MPDU 帧的数量。 802.11 工作站通过 802.11 MAC 标头的序列控件字段确定重复的帧。 如果每个端口无法维护此情况，则可以按通道进行维护。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站为 MSDU 数据包或 MMPDU 帧接收的 MPDU 帧的数量。</td>
</tr>
<tr class="even">
<td>UINT64</td>
<td>启用混杂数据包筛选器时，802.11 工作站接收的用于 MSDU 数据包或 MMPDU 帧的 MPDU 帧的数量。</td>
</tr>
<tr class="odd">
<td>UINT64</td>
<td>802.11 工作站收到并出现 FCS 错误的 MPDU 帧的数量。 如果每个端口无法维护此情况，则可以按通道进行维护。</td>
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

 

 




