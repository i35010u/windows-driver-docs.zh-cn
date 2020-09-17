---
title: 元数据字段标识符
description: 本部分介绍 Windows 筛选平台标注驱动程序的元数据字段标识符。
ms.assetid: 2157bace-9fae-41e8-a435-c4a412873ee1
keywords:
- 元数据字段标识符网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56e19633cb5505dc14382d2cbe7ccb39d1f76912
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714610"
---
# <a name="metadata-field-identifiers"></a>元数据字段标识符

每个元数据字段标识符由一个位域表示。 这些标识符定义如下：

<table>
<tr>
<th>
元数据字段标识符 
      </th>
<th>
说明 
      </th>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ALE_CLASSIFY_REQUIRED</p>
</td>
<td>
<p>入站数据包也会向 FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4 和 FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6 筛选层进行指示。</p>
<p>
<div class="alert"><b>注意</b>   Windows Server 2008、Windows Vista Service Pack 1 (SP1) 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_COMPARTMENT_ID</p>
</td>
<td>
<p>接收或发送数据包的路由隔离舱的标识符。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_COMPLETION_HANDLE</p>
</td>
<td>
<p>用于挂起当前筛选操作的完成句柄。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DESTINATION_INTERFACE_INDEX</p>
</td>
<td>
<p>要在其中发送传出数据包的网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DESTINATION_PREFIX</p>
</td>
<td>
<p>传出数据包的目标 IPV4 或 IPV6 地址和子网掩码。</p>
<div class="alert"><b>注意</b>   支持从 Windows 7 开始。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DISCARD_REASON</p>
</td>
<td>
<p>丢弃数据的原因。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ETHER_FRAME_LENGTH</p>
</td>
<td>
<p>此元数据字段标识符当前不受支持。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FLOW_HANDLE</p>
</td>
<td>
<p>数据流的句柄。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FORWARD_LAYER_INBOUND_PASS_THRU</p>
</td>
<td>
<p>遍历 FWPM_LAYER_IPFORWARD_V4 或 FWPM_LAYER_IPFORWARD_V6 转发层的数据包在本地 (其目标匹配分配给主机) 接口的地址。</p>
<p>
<div class="alert"><b>注意</b>   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FORWARD_LAYER_OUTBOUND_PASS_THRU</p>
</td>
<td>
<p>遍历 FWPM_LAYER_IPFORWARD_V4 或 FWPM_LAYER_IPFORWARD_V6 转发层的数据包在本地生成。</p>
<p>
<div class="alert"><b>注意</b>   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FRAGMENT_DATA</p>
</td>
<td>
<p>接收的数据包片段的片段数据。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ICMP_ID_AND_SEQUENCE</p>
</td>
<td>
<p>ICMP 回送请求或回显答复数据包的标识符和序列号字段。</p>
<p>
<div class="alert"><b>注意</b>   支持从 Windows 7 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_IP_HEADER_SIZE</p>
</td>
<td>
<p>IP 标头的大小。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_LOCAL_REDIRECT_TARGET_PID</p>
</td>
<td>
<p>连接已重定向到的进程 ID。</p>
<p>
<div class="alert"><b>注意</b>   支持从 Windows 7 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ORIGINAL_DESTINATION</p>
</td>
<td>
<p>一个 <a href="/windows/win32/api/ws2def/ns-ws2def-sockaddr_storage"><b>SOCKADDR_STORAGE</b></a> 结构，指示数据包的原始目标。</p>
<p>
<div class="alert"><b>注意</b>   支持从 Windows 7 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PACKET_DIRECTION</p>
</td>
<td>
<p>网络流量 (入站或出站) 的方向。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PACKET_SYSTEM_CRITICAL</p>
</td>
<td>
<p>预留给系统使用。 请勿使用。</p>
<p>
<div class="alert"><b>注意</b>   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PARENT_ENDPOINT_HANDLE</p>
</td>
<td>
<p>终结点的父套接字的句柄。</p>
<p>
<div class="alert"><b>注意</b>   支持从 Windows 7 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PATH_MTU</p>
</td>
<td>
<p>传出数据包 (路径 MTU) 路径最大传输单元。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PROCESS_ID</p>
</td>
<td>
<p>拥有终结点的进程的进程 ID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PROCESS_PATH</p>
</td>
<td>
<p>拥有终结点的进程的完整路径。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_REDIRECT_RECORD_HANDLE</p>
</td>
<td>
<p>"重定向记录" 句柄由分类元数据指定 ALE_CONNECT_REDIRECT 标注。</p>
<p>
<div class="alert"><b>注意</b>   从 Windows 8 开始支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_REMOTE_SCOPE_ID</p>
</td>
<td>
<p>要用于出站传输层注入的远程作用域标识符。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_RESERVED</p>
</td>
<td>
<p>预留给系统使用。 请勿使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SOURCE_INTERFACE_INDEX</p>
</td>
<td>
<p>接收传入数据包的网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SUB_PROCESS_TAG</p>
</td>
<td>
<p>预留给系统使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SYSTEM_FLAGS</p>
</td>
<td>
<p>筛选器引擎在内部使用的系统标志。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TOKEN</p>
</td>
<td>
<p>用于验证用户的权限的令牌。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_CONTROL_DATA</p>
</td>
<td>
<p>可选套接字控件数据对象。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_ENDPOINT_HANDLE</p>
</td>
<td>
<p>要注入到出站传输层的数据包末尾的句柄。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_HEADER_INCLUDE_HEADER</p>
</td>
<td>
<p>如果数据包是从原始套接字发送的，则为 IP 标头。</p>
<p>
<div class="alert"><b>注意</b>   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_HEADER_SIZE</p>
</td>
<td>
<p>传输标头的大小。</p>
</td>
</tr>
</table>