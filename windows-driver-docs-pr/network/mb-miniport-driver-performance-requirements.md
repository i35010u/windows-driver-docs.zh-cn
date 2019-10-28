---
title: MB 微型端口驱动程序性能要求
description: MB 微型端口驱动程序性能要求
ms.assetid: 16986208-7572-412d-8839-71f1a66b074f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 33ebb0720bed88b7add196dc84f88210bf2bf727
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844284"
---
# <a name="mb-miniport-driver-performance-requirements"></a>MB 微型端口驱动程序性能要求


下表描述了 MB 微型端口驱动程序对不同 MB 操作的响应。 为获得最佳体验，微型端口驱动程序应在 "最佳案例时间（秒）" 列中标识的时间内完成操作。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">MB 操作</th>
<th align="left">最佳案例时间（秒）</th>
<th align="left">最差的 case 时间（秒）</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>在插入到计算机后，要将设备初始化（以达到<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_ready_state" data-raw-source="[&lt;strong&gt;WwanReadyStateInitialized&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_ready_state)"><strong>WwanReadyStateInitialized</strong></a>）的时间（ <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info" data-raw-source="[OID_WWAN_READY_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)">OID_WWAN_READY_INFO</a>）</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>手动网络注册（ <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state" data-raw-source="[OID_WWAN_REGISTER_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-register-state)">OID_WWAN_REGISTER_STATE</a>）</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>50</p></td>
</tr>
<tr class="odd">
<td align="left"><p>网络扫描操作（ <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers" data-raw-source="[OID_WWAN_VISIBLE_PROVIDERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-visible-providers)">OID_WWAN_VISIBLE_PROVIDERS</a>）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>200</p></td>
</tr>
<tr class="even">
<td align="left"><p>数据包附加操作（ <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service" data-raw-source="[OID_WWAN_PACKET_SERVICE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-packet-service)">OID_WWAN_PACKET_SERVICE</a>）</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据包分离操作（OID_WWAN_PACKET_SERVICE）</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDP 激活（ <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect" data-raw-source="[OID_WWAN_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-connect)">OID_WWAN_CONNECT</a>）</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PDP 停用（OID_WWAN_CONNECT）</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>用 IP 地址、默认网关和 DNS 地址更新系统</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>启用 PDP 激活后的<a href="https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-link-state)"><strong>NDIS_STATUS_LINK_STATE</strong></a>通知</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>完成以下 PIN 操作（ <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin" data-raw-source="[OID_WWAN_PIN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin)">OID_WWAN_PIN</a>）：</p>
<p>Enter</p>
<p>Enable</p>
<p>禁用</p>
<p>“更改”</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>查询 OID_WWAN_PIN 以获取 MB 设备的当前 PIN 状态</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list" data-raw-source="[OID_WWAN_PIN_LIST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-pin-list)">OID_WWAN_PIN_LIST</a>响应以获取支持的 PIN 类型列表</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SMS 子系统准备就绪的时间（应发送 NDIS_STATUS_WWAN_SMS_CONFIGURATION 未经请求的指示）</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
<tr class="even">
<td align="left"><p>用于完成除 OID_WWAN_VENDOR_SPECIFIC 之外的所有其他 WWAN Oid （未在此表中介绍）的小型小型驱动程序的时间</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>15</p></td>
</tr>
</tbody>
</table>

 

 

 





