---
title: 元数据的字段标识符
description: 本部分介绍 Windows 筛选平台标注驱动程序的元数据字段标识符。
ms.assetid: 2157bace-9fae-41e8-a435-c4a412873ee1
keywords:
- 元数据的字段标识符网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 911c694f055009a584c929cf1451d4e8a035f8b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524187"
---
# <a name="metadata-field-identifiers"></a>元数据的字段标识符

每个由位字段的元数据字段标识符表示。 这些标识符定义，如下所示：

<table>
<tr>
<th>
元数据字段标识符 
      </th>
<th>
描述 
      </th>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ALE_CLASSIFY_REQUIRED</p>
</td>
<td>
<p>入站的数据包也将指向 FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4 和 FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6 筛选层。</p>
<p>
<div class="alert"><b>请注意</b>  支持在 Windows Server 2008 中，Windows Vista Service Pack 1 (SP1) 及更高版本。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_COMPARTMENT_ID</p>
</td>
<td>
<p>路由隔间收到或发送数据包的标识符。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_COMPLETION_HANDLE</p>
</td>
<td>
<p>使用完成句柄到挂起当前的筛选操作。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DESTINATION_INTERFACE_INDEX</p>
</td>
<td>
<p>将传出数据包将发送的网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DESTINATION_PREFIX</p>
</td>
<td>
<p>目标 IPV4 或 IPV6 地址和子网掩码的传出数据包。</p>
<div class="alert"><b>请注意</b>  支持从 Windows 7 开始。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_DISCARD_REASON</p>
</td>
<td>
<p>这些数据被丢弃的原因。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ETHER_FRAME_LENGTH</p>
</td>
<td>
<p>当前不支持此元数据字段标识符。</p>
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
<p>本地发往遍历 FWPM_LAYER_IPFORWARD_V4 或 FWPM_LAYER_IPFORWARD_V6 转发层的数据包 （其目标与分配给主机的接口的地址匹配）。</p>
<p>
<div class="alert"><b>请注意</b>  在 Windows Server 2008 中，Windows Vista sp1 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FORWARD_LAYER_OUTBOUND_PASS_THRU</p>
</td>
<td>
<p>遍历 FWPM_LAYER_IPFORWARD_V4 或 FWPM_LAYER_IPFORWARD_V6 的数据包将转发源自本地的层。</p>
<p>
<div class="alert"><b>请注意</b>  在 Windows Server 2008 中，Windows Vista sp1 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_FRAGMENT_DATA</p>
</td>
<td>
<p>接收的数据包片段片段数据。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ICMP_ID_AND_SEQUENCE</p>
</td>
<td>
<p>ICMP 回送请求或回送答复数据包的标识符和序列号的字段。</p>
<p>
<div class="alert"><b>请注意</b>  支持从 Windows 7 开始。</div>
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
<p>连接已重定向到进程 ID。</p>
<p>
<div class="alert"><b>请注意</b>  支持从 Windows 7 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_ORIGINAL_DESTINATION</p>
</td>
<td>
<p>一个<a href="https://msdn.microsoft.com/library/windows/hardware/ff570825"> <b>SOCKADDR_STORAGE</b> </a>指示数据包的结构&#39;s 原始目标。</p>
<p>
<div class="alert"><b>请注意</b>  支持从 Windows 7 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PACKET_DIRECTION</p>
</td>
<td>
<p>网络流量 （入站或出站） 的方向。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PACKET_SYSTEM_CRITICAL</p>
</td>
<td>
<p>保留供系统使用。 不使用。</p>
<p>
<div class="alert"><b>请注意</b>  在 Windows Server 2008 中，Windows Vista sp1 和更高版本中受支持。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PARENT_ENDPOINT_HANDLE</p>
</td>
<td>
<p>终结点的句柄&#39;s 父套接字。</p>
<p>
<div class="alert"><b>请注意</b>  支持从 Windows 7 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PATH_MTU</p>
</td>
<td>
<p>路径最大传输单元 （路径 MTU） 的传出数据包。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PROCESS_ID</p>
</td>
<td>
<p>拥有该终结点的进程的进程 ID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_PROCESS_PATH</p>
</td>
<td>
<p>拥有该终结点的进程的完整路径。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_REDIRECT_RECORD_HANDLE</p>
</td>
<td>
<p>重定向记录处理由为 ALE_CONNECT_REDIRECT 标注分类元数据。</p>
<p>
<div class="alert"><b>请注意</b>  支持从 Windows 8 开始。</div>
<div> </div>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_REMOTE_SCOPE_ID</p>
</td>
<td>
<p>要在出站传输层注入中使用的远程作用域标识符。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_RESERVED</p>
</td>
<td>
<p>保留供系统使用。 不使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SOURCE_INTERFACE_INDEX</p>
</td>
<td>
<p>在其中接收传入数据包的网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SUB_PROCESS_TAG</p>
</td>
<td>
<p>保留供系统使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_SYSTEM_FLAGS</p>
</td>
<td>
<p>系统由筛选器引擎在内部使用的标志。</p>
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
<p>一个可选的套接字控件的数据对象。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_ENDPOINT_HANDLE</p>
</td>
<td>
<p>对于要注入到出站传输层的数据包的结尾，句柄。</p>
</td>
</tr>
<tr>
<td>
<p>FWPS_METADATA_FIELD_TRANSPORT_HEADER_INCLUDE_HEADER</p>
</td>
<td>
<p>如果从原始套接字发送数据包 IP 标头之后。</p>
<p>
<div class="alert"><b>请注意</b>  在 Windows Server 2008 中，Windows Vista sp1 和更高版本中受支持。</div>
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

