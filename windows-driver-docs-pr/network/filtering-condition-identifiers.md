---
title: 筛选条件标识符
description: 本部分介绍筛选条件的标识符。
ms.assetid: 53321aea-6406-426a-a541-2626faad2232
keywords:
- 筛选条件标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: c30f766cbdb5349462a6ccdeec7941de278098d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353356"
---
# <a name="filtering-condition-identifiers"></a>筛选条件标识符

每个 guid 筛选条件标识符表示。 这些标识符是下表中所述。

<table>
<tr>
<th>筛选条件标识符</th>
<th>描述</th>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_INDEX</p>
</td>
<td>
<p>到达网络接口的枚举由网络堆栈的索引。</p>
<p>WFP 使用到达接口来匹配这种情况。 到达接口是之前执行弱主机或转发的数据包看到之前输入的 IP 堆栈入站网络中的第一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是入站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应出站数据包的入站的连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在到达接口条件的情况下接口条件的下一个跃点类将具有一个有效的接口在出站数据包数。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_TYPE</p>
</td>
<td>
<p>到达网络接口，通过 Internet 分配号机构 (IANA) 定义的类型。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定义</a>。</p>
<p>WFP 使用到达接口来匹配这种情况。 到达接口是之前执行弱主机或转发的数据包看到之前输入的 IP 堆栈入站网络中的第一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是入站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应出站数据包的入站的连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在到达接口条件的情况下接口条件的下一个跃点类将具有一个有效的接口在出站数据包数。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_TUNNEL_TYPE</p>
</td>
<td>
<p>如果使用隧道的封装方法的 IfType 成员<a href="https://docs.microsoft.com/windows/desktop/api/iptypes/ns-iptypes-_ip_adapter_addresses_lh"> <b>IP_ADAPTER_ADDRESSES</b> </a>结构是 IF_TYPE_TUNNEL。 隧道类型由 IANA 定义。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定义</a>和 Windows SDK <a href="https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper">IP 帮助程序</a>文档。</p>
<p>WFP 使用到达接口来匹配这种情况。 到达接口是之前执行弱主机或转发的数据包看到之前输入的 IP 堆栈入站网络中的第一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是入站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应出站数据包的入站的连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在到达接口条件的情况下接口条件的下一个跃点类将具有一个有效的接口在出站数据包数。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_ARRIVAL_INTERFACE</p>
</td>
<td>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/igpupvdev/ns-igpupvdev-_luid"> <b>LUID</b> </a>到达的 IP 地址相关联的网络接口。</p>
<p>WFP 使用到达接口来匹配这种情况。 到达接口是之前执行弱主机或转发的数据包看到之前输入的 IP 堆栈入站网络中的第一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是入站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应出站数据包的入站的连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在到达接口条件的情况下接口条件的下一个跃点类将具有一个有效的接口在出站数据包数。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_INDEX</p>
</td>
<td>
<p>到达网络接口的枚举由网络堆栈的索引。</p>
<p>WFP 使用下一跃点接口来匹配这种情况。 下一跃点接口是数据包执行弱主机或转发后，IP 堆栈离开网络，出站之前看到的最后一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是出站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应入站数据包的出站连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在下一跃点接口条件的情况下的接口条件到达类将拥有一个有效的接口上的入站数据包。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_TYPE</p>
</td>
<td>
<p>到达网络接口，通过 Internet 分配号机构 (IANA) 定义的类型。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定义</a>。</p>
<p>WFP 使用下一跃点接口来匹配这种情况。 下一跃点接口是数据包执行弱主机或转发后，IP 堆栈离开网络，出站之前看到的最后一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是出站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应入站数据包的出站连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在下一跃点接口条件的情况下的接口条件到达类将拥有一个有效的接口上的入站数据包。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_TUNNEL_TYPE</p>
</td>
<td>
<p>如果使用隧道的封装方法<b>IfType</b>的成员<a href="https://docs.microsoft.com/windows/desktop/api/iptypes/ns-iptypes-_ip_adapter_addresses_lh"> <b>IP_ADAPTER_ADDRESSES</b> </a>结构是 IF_TYPE_TUNNEL。 隧道类型由 IANA 定义。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType MIB 定义</a>和 Windows SDK <a href="https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper">IP 帮助程序</a>文档。</p>
<p>WFP 使用下一跃点接口来匹配这种情况。 下一跃点接口是数据包执行弱主机或转发后，IP 堆栈离开网络，出站之前看到的最后一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是出站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应入站数据包的出站连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在下一跃点接口条件的情况下的接口条件到达类将拥有一个有效的接口上的入站数据包。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_NEXTHOP_INTERFACE</p>
</td>
<td>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/igpupvdev/ns-igpupvdev-_luid"> <b>LUID</b></a>到达的 IP 地址相关联的网络接口。</p>
<p>WFP 使用下一跃点接口来匹配这种情况。 下一跃点接口是数据包执行弱主机或转发后，IP 堆栈离开网络，出站之前看到的最后一个接口。</p>
<p>这种情况是为了进行重新授权，非对称的因为它本质上是出站的条件。 这意味着 WFP，将对此条件中使用空值时正在对帐响应入站数据包的出站连接。</p>
<p>若要处理重新授权的第二个筛选器必须使用。 此第二个筛选器可以允许或阻止的空值，或使用一个不同的条件将具有此类情况的有效值。 在下一跃点接口条件的情况下的接口条件到达类将拥有一个有效的接口上的入站数据包。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、 Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS</p>
</td>
<td>
<p>本地 IP 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS</p>
</td>
<td>
<p>远程 IP 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_SOURCE_ADDRESS</p>
</td>
<td>
<p>转发的数据包的源 IP 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS</p>
</td>
<td>
<p>转发的数据包目标 IP 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>本地 IP 地址类型。 可能的条件值包括：</p>
<p>
<dl>
<dd>
NlatUnspecified

</dd>
<dd>
NlatUnicast

</dd>
<dd>
NlatAnycast

</dd>
<dd>
NlatMulticast

</dd>
<dd>
NlatBroadcast
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE</p>
</td>
<td>
<p>目标 IP 地址类型。 可能的条件值包括：</p>
<p>
<dl>
<dd>
NlatUnspecified

</dd>
<dd>
NlatUnicast

</dd>
<dd>
NlatAnycast

</dd>
<dd>
NlatMulticast

</dd>
<dd>
NlatBroadcast
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_INTERFACE</p>
</td>
<td>
<p>与本地 IP 地址关联的网络接口的 LUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_FORWARD_INTERFACE</p>
</td>
<td>
<p>网络接口转发的数据包是发出的 LUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
</td>
<td>
<p>IP 协议号中的规定<a href="https://tools.ietf.org/html/rfc1700">RFC 1700</a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_PORT</p>
</td>
<td>
<p>本地传输协议端口号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_PORT</p>
</td>
<td>
<p>远程传输协议端口号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ICMP_TYPE</p>
</td>
<td>
<p>ICMP 类型字段中指定<a href="https://tools.ietf.org/html/rfc792">RFC 792</a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ICMP_CODE</p>
</td>
<td>
<p>ICMP 代码字段中指定<a href="https://tools.ietf.org/html/rfc792">RFC 792</a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>本地 ICMP 数据包中嵌入的 IP 地址类型。 可能的条件值包括：</p>
<p>
<dl>
<dd>
NlatUnspecified

</dd>
<dd>
NlatUnicast

</dd>
<dd>
NlatAnycast

</dd>
<dd>
NlatMulticast

</dd>
<dd>
NlatBroadcast
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_ADDRESS</p>
</td>
<td>
<p>ICMP 数据包中嵌入远程 IP 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_PROTOCOL</p>
</td>
<td>
<p>嵌入在 ICMP 数据包中, 指定的 IP 协议号<a href="https://tools.ietf.org/html/rfc1700">RFC 1700</a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_PORT</p>
</td>
<td>
<p>嵌入在 ICMP 数据包本地传输协议端口号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_PORT</p>
</td>
<td>
<p>ICMP 数据包中嵌入远程传输协议端口号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_FLAGS</p>
</td>
<td>
<p>位或运算的筛选条件标志组合而成。 有关可能的标志的信息，请参阅<a href="filtering-condition-flags.md">筛选条件标志</a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DIRECTION</p>
</td>
<td>
<p>数据报数据或流量流的方向。</p>
<p>可能的条件值包括：</p>
<p>
<dl>
<dd>
FWP_DIRECTION_INBOUND

</dd>
<dd>
FWP_DIRECTION_OUTBOUND
</dd>
</dl>
</p>
<p>在数据报数据层和流数据包层中，这种情况指定数据包的方向。</p>
<p>在流层和 ALE 建立的流层中，此条件指定的连接 （例如，当连接，入站数据包已设置为 FWP_DIRECTION_OUTBOUND FWPM_CONDITION_DIRECTION 本地应用程序启动时） 的方向。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
</td>
<td>
<p>网络接口的枚举由网络堆栈的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_TYPE</p>
</td>
<td>
<p>网络接口的总线类型。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>逻辑网络接口的枚举由网络堆栈的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_INTERFACE_INDEX</p>
</td>
<td>
<p>转发的数据包，以枚举网络堆栈的源网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>转发的数据包，以枚举网络堆栈的源的逻辑网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_INTERFACE_INDEX</p>
</td>
<td>
<p>转发的数据包，以枚举网络堆栈的目标网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>转发的数据包，以枚举网络堆栈的目标的逻辑网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_APP_ID</p>
</td>
<td>
<p>应用程序的完整路径。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_USER_ID</p>
</td>
<td>
<p>本地用户的标识。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_REMOTE_USER_ID</p>
</td>
<td>
<p>远程用户的标识。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_REMOTE_MACHINE_ID</p>
</td>
<td>
<p>远程计算机的标识。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PROMISCUOUS_MODE</p>
</td>
<td>
<p>允许或拒绝原始套接字模式。 可能的条件值包括：</p>
<p>
<dl>
<dd>
SIO_RCVALL

</dd>
<dd>
SIO_RCVALL_IGMPMCAST

</dd>
<dd>
SIO_RCVALL_MCAST

</dd>
</dl>
</p>
<p>有关这些原始套接字模式的说明，请参阅<a href="https://docs.microsoft.com/windows/desktop/api/winsock2/nf-winsock2-wsaioctl"> <b>WSAIoctl</b> </a> Microsoft Windows SDK 文档中。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_SIO_FIREWALL_SYSTEM_PORT</p>
</td>
<td>
<p>保留供内部使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_NAP_CONTEXT</p>
</td>
<td>
<p>保留供内部使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_REMOTE_USER_TOKEN</p>
</td>
<td>
<p>远程用户的标识。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_IF_UUID</p>
</td>
<td>
<p>RPC 接口的 UUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_IF_VERSION</p>
</td>
<td>
<p>RPC 接口的版本。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RCP_IF_FLAG</p>
</td>
<td>
<p>保留供内部使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DCOM_APP_ID</p>
</td>
<td>
<p>COM 应用程序的标识。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IMAGE_NAME</p>
</td>
<td>
<p>应用程序的名称。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_PROTOCOL</p>
</td>
<td>
<p>RPC 协议。 可能的条件值包括：</p>
<p>
<dl>
<dd>
RPC_PROTSEQ_TCP

</dd>
<dd>
RPC_PROTSEQ_HTTP

</dd>
<dd>
RPC_PROTSEQ_NMP
</dd>
</dl>
</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_AUTH_TYPE</p>
</td>
<td>
<p>身份验证服务类型。 有关身份验证的服务类型的详细信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-service-constants"><b>身份验证服务常量</b></a> RPC 节的 Windows SDK 文档。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_AUTH_LEVEL</p>
</td>
<td>
<p>身份验证服务级别。 有关身份验证服务级别的详细信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-level-constants"><b>身份验证级别的常数</b></a> RPC 节的 Windows SDK 文档。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_ENCRYPT_ALGORITHM</p>
</td>
<td>
<p>基于证书的安全服务提供程序接口 (SSPI) 加密算法。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_KEY_SIZE</p>
</td>
<td>
<p>基于证书的安全服务提供程序接口 (SSPI) 加密密钥大小。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V4</p>
</td>
<td>
<p>本地的 IPv4 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V6</p>
</td>
<td>
<p>本地的 IPv6 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_PIPE</p>
</td>
<td>
<p>远程命名管道的名称。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V4</p>
</td>
<td>
<p>远程的 IPv4 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V6</p>
</td>
<td>
<p>远程的 IPv6 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_PROCESS_WITH_RPC_IF_UUID</p>
</td>
<td>
<p>使用 RPC 接口过程的 UUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_EP_VALUE</p>
</td>
<td>
<p>保留供内部使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_EP_FLAGS</p>
</td>
<td>
<p>保留供内部使用。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_TOKEN</p>
</td>
<td>
<p>使用 RpcProxy 时客户端的标识。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_SERVER_NAME</p>
</td>
<td>
<p>RPC 服务器时使用 RpcProxy 的名称。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_SERVER_PORT</p>
</td>
<td>
<p>RPC 服务器时使用 RpcProxy 上端口。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_PROXY_AUTH_TYPE</p>
</td>
<td>
<p>RPC 代理身份验证服务类型。 有关身份验证的服务类型的详细信息，请参阅<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-service-constants"><b>身份验证服务常量</b></a> RPC 节的 Windows SDK 文档。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
<td>
<p>使用隧道的封装方法。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_KEY_LENGTH</p>
</td>
<td>
<p>安全套接字层 (SSL) 密钥中的客户端证书的长度。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_OID</p>
</td>
<td>
<p>在客户端证书对象标识符 (OID)。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_MAC_ADDRESS
</p>
</td>
<td>
<p>发送或接收网络接口的物理地址。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_LOCAL_ADDRESS
</p>
</td>
<td>
<p>本地网络接口的物理地址。
为入站流量，这是目标框架中的 MAC 地址。
为出站流量，这是源帧的 MAC 地址。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS</p>
</td>
<td>
<p>远程网络接口的物理地址。
为入站流量，这是源帧中的 MAC 地址。
为出站流量，这是框架的目标 MAC 地址。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ETHER_TYPE</p>
</td>
<td>
<p>在 MAC 帧中指示的类型。
此值是为 IPv4 流量 0x800 0x86DD IPv6 流量或 0x806 ARP 流量。
所有可能的值被定义为 NDIS_ETH_TYPE_Xxx ntddndis.h 中。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VLAN_ID</p>
</td>
<td>
<p>VLAN 在以太网对齐标头中的标识符。
如果框架的以太网 ii 型，则此值为 0。
</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PORT</p>
</td>
<td>
<p>确定微型端口适配器端口的端口号。 </p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_MEDIA_TYPE</p>
</td>
<td>
<p>类型指定为其中一个的 NDIS 介质<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_medium"> <b>NDIS_MEDIUM</b> </a>枚举值。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PHYSICAL_MEDIA_TYPE</p>
</td>
<td>
<p>指定为 NDIS_PHYSICAL_MEDIUM 枚举值之一的通信接口使用的物理介质的类型。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_L2_FLAGS</p>
</td>
<td>
<p>位或运算的筛选条件 MAC 层的标志组合而成。 有关可能的标志的信息，请参阅<a href="filtering-condition-l2-flags.md">筛选条件 L2 标志</a>。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>数据链接的本地 MAC 地址类型。 这是在中定义的值之一<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h 中的枚举。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS_TYPE</p>
</td>
<td>
<p>数据链接类型的远程 MAC 地址。 这是在中定义的值之一<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h 中的枚举。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE</p>
</td>
<td>
<p>与本地 MAC 地址关联的网络接口的 LUID。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>AppContainer 受限包安全标识符 (SID)。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS</p>
</td>
<td>
<p>创建 MAC 帧的网络接口物理地址。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS</p>
</td>
<td>
<p>帧发送到该网络接口的物理地址。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS_TYPE</p>
</td>
<td>
<p>数据链接创建帧的接口的 MAC 地址类型。 这是在中定义的值之一<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h 中的枚举。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS_TYPE</p>
</td>
<td>
<p>数据链接到的目标框架的接口的 MAC 地址类型。 这是在中定义的值之一<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"> <b>DL_ADDRESS_TYPE</b> </a> FwpmTypes.h 中的枚举。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_SOURCE_PORT</p>
</td>
<td>
<p>传输协议的源端口号。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_PORT</p>
</td>
<td>
<p>传输协议目标端口号。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_ID</p>
</td>
<td>
<p>虚拟交换机的 GUID。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_NETWORK_TYPE</p>
</td>
<td>
<p>与虚拟交换机相关联的网络的类型。 这是在中定义的值之一<a href="https://docs.microsoft.com/windows/desktop/api/fwptypes/ne-fwptypes-fwp_vswitch_network_type_"> <b>FWP_VSWITCH_NETWORK_TYPE</b> </a> FwpTypes.h 中的枚举。</p>
<div class="alert"><b>请注意</b>中支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID</p>
</td>
<td>
<p>创建框架的虚拟交换机的接口的 GUID。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_ID</p>
</td>
<td>
<p>虚拟接口的 GUID 的切换到帧发送到。</p>
<div class="alert"><b>请注意</b>中支持<i>Windows 8</i>和更高版本的 Windows。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE</p>
</td>
<td>
<p>创建框架的虚拟交换机接口的类型。 这是在中定义的值之一<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_nic_switch_type"> <b>NDIS_NIC_SWITCH_TYPE</b> </a> Ntddndis.h 中的枚举。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_TYPE</p>
</td>
<td>
<p>向其发送到帧的虚拟交换机接口的类型。 这是在中定义的值之一<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ne-ntddndis-_ndis_nic_switch_type"> <b>NDIS_NIC_SWITCH_TYPE</b> </a> Ntddndis.h 中的枚举。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
</td>
<td>
<p>VSwitch 源虚拟机的唯一标识符。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_VM_ID</p>
</td>
<td>
<p>VSwitch 目标虚拟机的唯一标识符。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
</td>
<td>
<p>VSwitch 网络的的唯一标识符。 不能与 VLAN_IDs 结合使用。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>应用程序容器安全标识符 (SID)。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_ORIGINAL_APP_ID</p>
</td>
<td>
<p>从代理的更改之前在应用程序的原始完整路径。  请注意，是否不涉及代理，则这将 FWPM_CONDITION_ALE_APP_ID 相同。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_QM_MODE</p>
</td>
<td>
<p>快速模式 (QM) 模式中。</p>
<div class="alert"><b>请注意</b>Windows 8、 Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
</table>

