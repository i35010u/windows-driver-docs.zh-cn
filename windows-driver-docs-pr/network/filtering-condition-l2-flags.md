---
title: 筛选条件 L2 标志
description: 本部分介绍筛选条件 L2 标志。
keywords:
- 筛选条件 L2 标志网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7779f6ed66df3eb2e38ffec0455960ed48f6c31
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825525"
---
# <a name="filtering-condition-l2-flags"></a>筛选条件 L2 标志

筛选条件 L2 标志分别由位域表示。 这些标志定义如下：

<table>
<tr>
<th>筛选条件标志</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_NATIVE_ETHERNET</p>
<p>0x00000001</p>
</td>
<td>
<p>测试传递给标注驱动程序的数据是否描述了本机以太网数据包。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
<p>测试传递给标注驱动程序的数据是否描述了 WIFI 数据包。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_WIFI</p>
<p>0x00000002</p>
</td>
<td>
<p>测试传递给标注驱动程序的数据是否描述了本机 Wi-Fi 数据包。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_MOBILE_BROADBAND</p>
<p>0x00000004</p>
</td>
<td>
<p>测试传递给标注驱动程序的数据是否描述了移动宽带数据包。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_WIFI_DIRECT_DATA</p>
<p>0x00000008</p>
</td>
<td>
<p>测试传递给标注驱动程序的数据是否描述了 WIFI 直接数据包。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_VM2VM</p>
<p>0x00000010</p>
</td>
<td>
<p>测试传递给标注驱动程序的数据是否将本机虚拟机描述为虚拟机数据包。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_MALFORMED_PACKET</p>
<p>0x00000020</p>
</td>
<td>
<p>测试传递给标注驱动程序的数据是否描述了格式错误的以太网数据包。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IS_IP_FRAGMENT_GROUP</p>
<p>0x00000040</p>
</td>
<td>
<p>测试传递给标注驱动程序的数据是否描述了 IP 片段组的一部分。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
<tr>
<td>
<p>FWP_CONDITION_L2_IF_CONNECTOR_PRESENT</p>
<p>0x00000080</p>
</td>
<td>
<p>测试基础网络适配器上是否存在网络接口连接器。</p>
<p>应为物理适配器设置此标志。</p>
<p>此标志适用于 windows 8、Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
<dl>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET
</dd>
<dd>
FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE
</dd>
<dd>
FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE
</dd>
</dl>
</td>
</tr>
</table>

