---
title: 筛选条件 L2 标志
description: 本部分介绍筛选条件 L2 标志。
ms.assetid: D24A261D-6324-43CC-BD2A-CDB9B024432C
keywords:
- 筛选条件 L2 标志网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7571f114a4a0fecc6371215441aaf9b4153c8e84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347525"
---
# <a name="filtering-condition-l2-flags"></a>筛选条件 L2 标志

每个表示位域的筛选条件 L2 标志。 这些标志定义，如下所示：

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
<p>如果将数据传递给标注驱动程序测试介绍本机的以太网数据包。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>如果将数据传递给标注驱动程序测试介绍 WIFI 数据包。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>如果将数据传递给标注驱动程序测试介绍本机 Wi-fi 数据包。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>如果将数据传递给标注驱动程序测试介绍移动宽带数据包。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>如果传递给标注驱动程序的数据描述 WIFI 的测试直接数据包。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>如果将数据传递给标注驱动程序测试介绍本机虚拟机到虚拟机数据包。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>如果将数据传递给标注驱动程序测试描述格式不正确的以太网数据包。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>如果将数据传递给标注驱动程序测试介绍 IP 片段组的一部分。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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
<p>测试网络接口连接器是否存在于基础网络适配器上。</p>
<p>应为物理适配器设置此标志。</p>
<p>此标志是适用于 Windows 8、 Windows Server 2012 和更高版本的 Windows 中的以下筛选层：</p>
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

