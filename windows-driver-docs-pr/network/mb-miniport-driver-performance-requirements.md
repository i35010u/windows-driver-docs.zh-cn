---
title: MB 微型端口驱动程序性能要求
description: MB 微型端口驱动程序性能要求
ms.assetid: 16986208-7572-412d-8839-71f1a66b074f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7cc897488d143b7fe69bbfbe17dba3115dcd970
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343295"
---
# <a name="mb-miniport-driver-performance-requirements"></a>MB 微型端口驱动程序性能要求


下表介绍 MB 微型端口驱动程序以不同 MB 操作响应的期望。 为获得最佳体验，微型端口驱动程序应在"最好的条件时间 （秒）"列中标识的时间内完成操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MB 操作</th>
<th align="left">最佳事例时间 （秒）</th>
<th align="left">最差事例时间 （秒）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>设备初始化时间 (以达到<a href="https://msdn.microsoft.com/library/windows/hardware/ff571227" data-raw-source="[&lt;strong&gt;WwanReadyStateInitialized&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff571227)"> <strong>WwanReadyStateInitialized</strong></a>) 后插入到计算机 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569833" data-raw-source="[OID_WWAN_READY_INFO](https://msdn.microsoft.com/library/windows/hardware/ff569833)">OID_WWAN_READY_INFO</a>)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>手动网络注册 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569834" data-raw-source="[OID_WWAN_REGISTER_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569834)">OID_WWAN_REGISTER_STATE</a>)</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>50</p></td>
</tr>
<tr class="odd">
<td align="left"><p>网络扫描操作 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569843" data-raw-source="[OID_WWAN_VISIBLE_PROVIDERS](https://msdn.microsoft.com/library/windows/hardware/ff569843)">OID_WWAN_VISIBLE_PROVIDERS</a>)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>200</p></td>
</tr>
<tr class="even">
<td align="left"><p>数据包附加操作 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569827" data-raw-source="[OID_WWAN_PACKET_SERVICE](https://msdn.microsoft.com/library/windows/hardware/ff569827)">OID_WWAN_PACKET_SERVICE</a>)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据包分离操作 (OID_WWAN_PACKET_SERVICE)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDP 激活 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569823" data-raw-source="[OID_WWAN_CONNECT](https://msdn.microsoft.com/library/windows/hardware/ff569823)">OID_WWAN_CONNECT</a>)</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PDP 停用 (OID_WWAN_CONNECT)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>使用 IP 地址、 默认网关和 DNS 地址来更新系统</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567391" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567391)"><strong>NDIS_STATUS_LINK_STATE</strong> </a> PDP 激活后的通知</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>以下固定操作完成的 ( <a href="https://msdn.microsoft.com/library/windows/hardware/ff569828" data-raw-source="[OID_WWAN_PIN](https://msdn.microsoft.com/library/windows/hardware/ff569828)">OID_WWAN_PIN</a>):</p>
<p>Enter</p>
<p>启用</p>
<p>禁用</p>
<p>“更改”</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>查询 OID_WWAN_PIN 若要获取的 MB 设备的当前 PIN 状态</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569829" data-raw-source="[OID_WWAN_PIN_LIST](https://msdn.microsoft.com/library/windows/hardware/ff569829)">OID_WWAN_PIN_LIST</a>获取一系列响应支持的 PIN 类型</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>短信子系统才能准备就绪的时间 (应发送 NDIS_STATUS_WWAN_SMS_CONFIGURATION 未经请求的指示)</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
<tr class="even">
<td align="left"><p>若要完成所有其他 WWAN Oid OID_WWAN_VENDOR_SPECIFIC 除此表中未涉及的微型端口驱动程序的时间</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>15</p></td>
</tr>
</tbody>
</table>

 

 

 





