---
title: 筛选条件标识符
description: 本部分介绍筛选条件标识符。
ms.assetid: 53321aea-6406-426a-a541-2626faad2232
keywords:
- 筛选条件标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ea3f46571580afaff1a6e6c4f2ad5b8af392495
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833764"
---
# <a name="filtering-condition-identifiers"></a>筛选条件标识符

筛选条件标识符由 GUID 表示。 下表对这些标识符进行了说明。

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
<p>网络堆栈枚举的到达网络接口的索引。</p>
<p>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_INTERFACE_TYPE</p>
</td>
<td>
<p>由 Internet 号码分配机构（IANA）定义的到达网络接口的类型。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType 定义</a>。</p>
<p>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ARRIVAL_TUNNEL_TYPE</p>
</td>
<td>
<p>如果<a href="https://docs.microsoft.com/windows/desktop/api/iptypes/ns-iptypes-_ip_adapter_addresses_lh"><b>IP_ADAPTER_ADDRESSES</b></a>结构的 IfType 成员为 IF_TYPE_TUNNEL，则为隧道使用的封装方法。 隧道类型由 IANA 定义。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType 定义</a>和 Windows SDK <a href="https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper">IP 帮助器</a>文档。</p>
<p>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_ARRIVAL_INTERFACE</p>
</td>
<td>
<p>与到达 IP 地址关联的网络接口的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid"><b>LUID</b></a> 。</p>
<p>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_INDEX</p>
</td>
<td>
<p>网络堆栈枚举的到达网络接口的索引。</p>
<p>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_INTERFACE_TYPE</p>
</td>
<td>
<p>由 Internet 号码分配机构（IANA）定义的到达网络接口的类型。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType 定义</a>。</p>
<p>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NEXTHOP_TUNNEL_TYPE</p>
</td>
<td>
<p>如果<a href="https://docs.microsoft.com/windows/desktop/api/iptypes/ns-iptypes-_ip_adapter_addresses_lh"><b>IP_ADAPTER_ADDRESSES</b></a>结构的<b>IFTYPE</b>成员为 IF_TYPE_TUNNEL，则为隧道使用的封装方法。 隧道类型由 IANA 定义。 有关详细信息，请参阅<a href="http://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib">IANAifType 定义</a>和 Windows SDK <a href="https://docs.microsoft.com/windows-hardware/drivers/network/ip-helper">IP 帮助器</a>文档。</p>
<p>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_NEXTHOP_INTERFACE</p>
</td>
<td>
<p>与到达 IP 地址关联的网络接口的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid"><b>LUID</b></a>。</p>
<p>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</p>
<p>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</p>
<p>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</p>
<div class="alert"><b>注意</b><br/>仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。
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
<p>转发的数据包的目标 IP 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>本地 IP 地址类型。 可能的条件值为：</p>
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
<p>目标 IP 地址类型。 可能的条件值为：</p>
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
<p>要向其发送数据包的网络接口的 LUID。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_PROTOCOL</p>
</td>
<td>
<p><a href="https://tools.ietf.org/html/rfc1700">RFC 1700</a>中指定的 IP 协议号。</p>
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
<p>在<a href="https://tools.ietf.org/html/rfc792">RFC 792</a>中指定的 "ICMP 类型" 字段。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ICMP_CODE</p>
</td>
<td>
<p>在<a href="https://tools.ietf.org/html/rfc792">RFC 792</a>中指定的 "ICMP 代码" 字段。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>在 ICMP 数据包中嵌入的本地 IP 地址类型。 可能的条件值为：</p>
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
<p>嵌入 ICMP 数据包的远程 IP 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_PROTOCOL</p>
</td>
<td>
<p>在 ICMP 数据包中嵌入的 IP 协议号，如<a href="https://tools.ietf.org/html/rfc1700">RFC 1700</a>中所指定。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_LOCAL_PORT</p>
</td>
<td>
<p>在 ICMP 数据包中嵌入的本地传输协议端口号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_EMBEDDED_REMOTE_PORT</p>
</td>
<td>
<p>在 ICMP 数据包中嵌入的远程传输协议端口号。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_FLAGS</p>
</td>
<td>
<p>筛选条件标志的组合的按位 "或"。 有关可能的标志的信息，请参阅<a href="filtering-condition-flags.md">筛选条件标志</a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DIRECTION</p>
</td>
<td>
<p>数据报流量或数据流的方向。</p>
<p>可能的条件值为：</p>
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
<p>在数据报数据层和流数据包层中，此条件指定数据包的方向。</p>
<p>在流层和 ALE 流建立的层中，此条件指定连接的方向（例如，当本地应用程序启动连接时，入站数据包的 FWPM_CONDITION_DIRECTION 设置为 FWP_DIRECTION_OUTBOUND）。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_INDEX</p>
</td>
<td>
<p>网络堆栈枚举的网络接口的索引。</p>
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
<p>由网络堆栈枚举的逻辑网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_INTERFACE_INDEX</p>
</td>
<td>
<p>网络堆栈枚举的转发数据包的源网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SOURCE_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>网络堆栈枚举的转发数据包的源逻辑网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_INTERFACE_INDEX</p>
</td>
<td>
<p>网络堆栈枚举的转发数据包的目标网络接口的索引。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_DESTINATION_SUB_INTERFACE_INDEX</p>
</td>
<td>
<p>网络堆栈枚举的转发数据包的目标逻辑网络接口的索引。</p>
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
<p>允许或拒绝的原始套接字模式。 可能的条件值为：</p>
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
<p>有关这些原始套接字模式的说明，请参阅 Microsoft Windows SDK 文档中的<a href="https://docs.microsoft.com/windows/desktop/api/winsock2/nf-winsock2-wsaioctl"><b>WSAIoctl</b></a> 。</p>
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
<p>RPC 协议。 可能的条件值为：</p>
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
<p>身份验证服务类型。 有关身份验证服务类型的详细信息，请参阅 Windows SDK 文档的 RPC 部分中的<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-service-constants"><b>身份验证-服务常量</b></a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_AUTH_LEVEL</p>
</td>
<td>
<p>身份验证服务级别。 有关身份验证服务级别的详细信息，请参阅 Windows SDK 文档的 RPC 部分中的<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-level-constants"><b>身份验证级别常量</b></a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_ENCRYPT_ALGORITHM</p>
</td>
<td>
<p>基于证书的安全服务提供程序接口（SSPI）加密算法。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_SEC_KEY_SIZE</p>
</td>
<td>
<p>基于证书的安全服务提供程序接口（SSPI）加密密钥大小。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V4</p>
</td>
<td>
<p>本地 IPv4 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_LOCAL_ADDRESS_V6</p>
</td>
<td>
<p>本地 IPv6 地址。</p>
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
<p>远程 IPv4 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_REMOTE_ADDRESS_V6</p>
</td>
<td>
<p>远程 IPv6 地址。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_PROCESS_WITH_RPC_IF_UUID</p>
</td>
<td>
<p>具有 RPC 接口的进程的 UUID。</p>
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
<p>RPC 服务器的名称（使用 RpcProxy 时）。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_SERVER_PORT</p>
</td>
<td>
<p>使用 RpcProxy 时 RPC 服务器上的端口。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_RPC_PROXY_AUTH_TYPE</p>
</td>
<td>
<p>RPC 代理身份验证服务类型。 有关身份验证服务类型的详细信息，请参阅 Windows SDK 文档的 RPC 部分中的<a href="https://docs.microsoft.com/windows/desktop/Rpc/authentication-service-constants"><b>身份验证-服务常量</b></a>。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_TUNNEL_TYPE</p>
</td>
<td>
<p>隧道使用的封装方法。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_KEY_LENGTH</p>
</td>
<td>
<p>客户端证书中的安全套接字层（SSL）密钥长度。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_CLIENT_CERT_OID</p>
</td>
<td>
<p>客户端证书中的对象标识符（OID）。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE_MAC_ADDRESS
</p>
</td>
<td>
<p>发送或接收网络接口的物理地址。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
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
对于入站流量，这是帧中的目标 MAC 地址。
对于出站流量，这是帧的源 MAC 地址。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS</p>
</td>
<td>
<p>远程网络接口的物理地址。
对于入站流量，这是帧中的源 MAC 地址。
对于出站流量，这是帧的目标 MAC 地址。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ETHER_TYPE</p>
</td>
<td>
<p>MAC 帧中指示的类型。
对于 IPv4 流量，此值为0x800，对于 IPv6 流量为0x86DD，对于 ARP 流量为0x806。
所有可能的值都在 ntddndis 中定义为 NDIS_ETH_TYPE_Xxx。</p>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VLAN_ID</p>
</td>
<td>
<p>以太网 SNAP 标头中 VLAN 的标识符。
如果帧是以太网 II，则此值为0。
</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PORT</p>
</td>
<td>
<p>标识微型端口适配器端口的端口号。 </p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_MEDIA_TYPE</p>
</td>
<td>
<p>指定为<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_medium"><b>NDIS_MEDIUM</b></a>枚举值之一的 NDIS 介质的类型。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_NDIS_PHYSICAL_MEDIA_TYPE</p>
</td>
<td>
<p>指定为 NDIS_PHYSICAL_MEDIUM 枚举值之一的通信接口的物理介质的类型。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_L2_FLAGS</p>
</td>
<td>
<p>用于 MAC 层的筛选条件标志组合的按位 "或"。 有关可能的标志的信息，请参阅<a href="filtering-condition-l2-flags.md">筛选条件 L2 标志</a>。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_LOCAL_ADDRESS_TYPE</p>
</td>
<td>
<p>本地 MAC 地址的链接类型。 这是在 FwpmTypes 的<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>枚举中定义的值之一。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_REMOTE_ADDRESS_TYPE</p>
</td>
<td>
<p>远程 MAC 地址的链接类型。 这是在 FwpmTypes 的<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>枚举中定义的值之一。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_INTERFACE</p>
</td>
<td>
<p>与本地 MAC 地址关联的网络接口的 LUID。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>AppContainer 受限包的安全标识符（SID）。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS</p>
</td>
<td>
<p>创建 MAC 帧的网络接口的物理地址。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS</p>
</td>
<td>
<p>帧的目标网络接口的物理地址。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_SOURCE_ADDRESS_TYPE</p>
</td>
<td>
<p>创建该帧的接口的 MAC 地址的链接类型。 这是在 FwpmTypes 的<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>枚举中定义的值之一。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_MAC_DESTINATION_ADDRESS_TYPE</p>
</td>
<td>
<p>帧的目标接口的 MAC 地址的链接类型。 这是在 FwpmTypes 的<a href="https://docs.microsoft.com/windows/desktop/api/fwpmtypes/ne-fwpmtypes-__midl___midl_itf_fwpmtypes_0000_0000_0001"><b>DL_ADDRESS_TYPE</b></a>枚举中定义的值之一。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_SOURCE_PORT</p>
</td>
<td>
<p>传输协议源端口号。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_IP_DESTINATION_PORT</p>
</td>
<td>
<p>传输协议目标端口号。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_ID</p>
</td>
<td>
<p>虚拟交换机的 GUID。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_NETWORK_TYPE</p>
</td>
<td>
<p>与虚拟交换机关联的网络的类型。 这是在 FwpTypes 的<a href="https://docs.microsoft.com/windows/desktop/api/fwptypes/ne-fwptypes-fwp_vswitch_network_type_"><b>FWP_VSWITCH_NETWORK_TYPE</b></a>枚举中定义的值之一。</p>
<div class="alert"><b>注意</b> 在 windows <i>8</i>和更高版本的 windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID</p>
</td>
<td>
<p>创建该帧的虚拟交换机的接口的 GUID。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_ID</p>
</td>
<td>
<p>帧所指向的虚拟交换机的接口的 GUID。</p>
<div class="alert"><b>注意</b> 在 windows <i>8</i>和更高版本的 windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE</p>
</td>
<td>
<p>创建该帧的虚拟交换机接口的类型。 这是在 Ntddndis 的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_nic_switch_type"><b>NDIS_NIC_SWITCH_TYPE</b></a>枚举中定义的值之一。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_TYPE</p>
</td>
<td>
<p>帧的目标虚拟交换机接口的类型。 这是在 Ntddndis 的<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_nic_switch_type"><b>NDIS_NIC_SWITCH_TYPE</b></a>枚举中定义的值之一。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_SOURCE_VM_ID</p>
</td>
<td>
<p>VSwitch 源虚拟机的唯一标识符。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_DESTINATION_VM_ID</p>
</td>
<td>
<p>VSwitch 目标虚拟机的唯一标识符。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID</p>
</td>
<td>
<p>VSwitch 网络的唯一标识符。 不能与 VLAN_IDs 一起使用。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_PACKAGE_ID</p>
</td>
<td>
<p>应用容器的安全标识符（SID）。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_ALE_ORIGINAL_APP_ID</p>
</td>
<td>
<p>在从代理更改之前，应用程序的原始完整路径。  请注意，如果不涉及代理，则这将与 FWPM_CONDITION_ALE_APP_ID 相同。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
<tr>
<td>
<p>FWPM_CONDITION_QM_MODE</p>
</td>
<td>
<p>快速模式（QM）模式。</p>
<div class="alert"><b>注意</b> 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。</div>
<div> </div>
</td>
</tr>
</table>

