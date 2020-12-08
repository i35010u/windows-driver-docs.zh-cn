---
title: 筛选条件标识符
description: 本部分介绍筛选条件标识符。
keywords:
- 筛选条件标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4a687f57ce53bbaa5c240f69e33b69f697079c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825537"
---
# <a name="filtering-condition-identifiers"></a>筛选条件标识符

筛选条件标识符由 GUID 表示。 下表对这些标识符进行了说明。

|筛选条件标识符|描述|
|----|----|
|FWPM_CONDITION_ARRIVAL_INTERFACE_INDEX|网络堆栈枚举的到达网络接口的索引。</br>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</br>请注意，此功能仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。|
|FWPM_CONDITION_ARRIVAL_INTERFACE_TYPE|由 Internet 分配的编号颁发机构 (IANA) 定义的到达网络接口的类型。 有关详细信息，请参阅 [IANAifType 定义](https://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib)。</br>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</br>请注意，这只在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中 v。|
|FWPM_CONDITION_ARRIVAL_TUNNEL_TYPE|如果 IF_TYPE_TUNNEL [IP_ADAPTER_ADDRESSES](/windows/win32/api/iptypes/ns-iptypes-ip_adapter_addresses_lh) 结构的 IfType 成员，则为隧道使用的封装方法。 隧道类型由 IANA 定义。 有关详细信息，请参阅 [IANAifType 定义](https://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib) 和 Windows SDK [IP 帮助器](./ip-helper.md) 文档。</br>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</br>请注意，此功能仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。|
|FWPM_CONDITION_IP_ARRIVAL_INTERFACE|与到达 IP 地址关联的网络接口的 [LUID](/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid) 。</br>WFP 使用到达接口来匹配此条件。 到达接口是在执行弱主机或转发之前，从网络进入 IP 堆栈入站之前，数据包看到的第一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它本身就是入站条件。 这意味着，当延伸响应出站数据包上的入站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 如果到达接口条件，接口条件的下一个跃点类将在出站数据包上具有有效接口。</br>请注意，此功能仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。|
|FWPM_CONDITION_NEXTHOP_INTERFACE_INDEX|网络堆栈枚举的到达网络接口的索引。</br>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</br>请注意，此功能仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。|
|FWPM_CONDITION_NEXTHOP_INTERFACE_TYPE|由 Internet 分配的编号颁发机构 (IANA) 定义的到达网络接口的类型。 有关详细信息，请参阅 [IANAifType 定义](https://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib)。</br>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</br>请注意，此功能仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。|
|FWPM_CONDITION_NEXTHOP_TUNNEL_TYPE|如果 IF_TYPE_TUNNEL [**IP_ADAPTER_ADDRESSES**](/windows/win32/api/iptypes/ns-iptypes-ip_adapter_addresses_lh)结构的 **IfType** 成员，则为隧道使用的封装方法。 隧道类型由 IANA 定义。 有关详细信息，请参阅 [IANAifType 定义](https://www.iana.org/assignments/ianaiftype-mib/ianaiftype-mib) 和 Windows SDK [IP 帮助器](./ip-helper.md) 文档。</br>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</br>请注意，此功能仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。|
|FWPM_CONDITION_IP_NEXTHOP_INTERFACE|与到达 IP 邮件关联的网络接口的[LUID](/windows-hardware/drivers/ddi/igpupvdev/ns-igpupvdev-_luid)</br>WFP 使用下一个跃点接口来匹配此条件。 下一个跃点接口是在执行弱主机或转发后，将 IP 堆栈向网络传出之前，数据包所看到的最后一个接口。</br>出于重新授权目的，这种情况是不对称的，因为它是固有的出站条件。 这意味着，当延伸响应入站数据包上的出站连接时，WFP 将对此条件使用空值。</br>若要处理重新授权，必须使用第二个筛选器。 此第二个筛选器可以允许或阻止空值，也可以使用在这种情况下具有有效值的不同条件。 对于下一个跃点接口条件，接口条件的到达类将在入站数据包上具有有效接口。</br>请注意，此功能仅在 Windows Server 2008 R2、Windows 7 和更高版本的 Windows 中可用。|
|FWPM_CONDITION_IP_LOCAL_ADDRESS|本地 IP 地址。|
|FWPM_CONDITION_IP_REMOTE_ADDRESS|远程 IP 地址。|
|FWPM_CONDITION_IP_SOURCE_ADDRESS|转发的数据包的源 IP 地址。|
|FWPM_CONDITION_IP_DESTINATION_ADDRESS|转发的数据包的目标 IP 地址。|
|FWPM_CONDITION_IP_LOCAL_ADDRESS_TYPE|本地 IP 地址类型。 可能的条件值为：</br>- NlatUnspecified</br>- NlatUnicast</br>- NlatAnycast</br>- NlatMulticast</br>- NlatBroadcast|
|FWPM_CONDITION_IP_DESTINATION_ADDRESS_TYPE|目标 IP 地址类型。 可能的条件值为：</br>- NlatUnspecified</br>- NlatUnicast</br>- NlatAnycast</br>- NlatMulticast</br>- NlatBroadcast|
|FWPM_CONDITION_IP_LOCAL_INTERFACE|与本地 IP 地址关联的网络接口的 LUID。|
|FWPM_CONDITION_IP_FORWARD_INTERFACE|要向其发送数据包的网络接口的 LUID。|
|FWPM_CONDITION_IP_PROTOCOL|[RFC 1700](https://tools.ietf.org/html/rfc1700)中指定的 IP 协议号。|
|FWPM_CONDITION_IP_LOCAL_PORT|本地传输协议端口号。|
|FWPM_CONDITION_IP_REMOTE_PORT|远程传输协议端口 |编号。|
|FWPM_CONDITION_ICMP_TYPE|在 [RFC 792](https://tools.ietf.org/html/rfc792)中指定的 "ICMP 类型" 字段。|
|FWPM_CONDITION_ICMP_CODE|在 [RFC 792](https://tools.ietf.org/html/rfc792)中指定的 "ICMP 代码" 字段。|
|FWPM_CONDITION_EMBEDDED_LOCAL_ADDRESS_TYPE|在 ICMP 数据包中嵌入的本地 IP 地址类型。 可能的条件值为：</br>- NlatUnspecified</br>- NlatUnicast</br>- NlatAnycast</br>- NlatMulticast</br>- NlatBroadcast|
|FWPM_CONDITION_EMBEDDED_REMOTE_ADDRESS|嵌入 ICMP 数据包的远程 IP 地址。|
|FWPM_CONDITION_EMBEDDED_PROTOCOL|在 ICMP 数据包中嵌入的 IP 协议号，如 [RFC 1700](https://tools.ietf.org/html/rfc1700)中所指定。|
|FWPM_CONDITION_EMBEDDED_LOCAL_PORT|在 ICMP 数据包中嵌入的本地传输协议端口号。|
|FWPM_CONDITION_EMBEDDED_REMOTE_PORT|在 ICMP 数据包中嵌入的远程传输协议端口号。|
|FWPM_CONDITION_FLAGS|筛选条件标志的组合的按位 "或"。 有关可能的标志的信息，请参阅 [筛选条件标志](filtering-condition-flags.md)。|
|FWPM_CONDITION_DIRECTION|数据报流量或数据流的方向。 可能的条件值为：</br>-FWP_DIRECTION_INBOUND</br>-FWP_DIRECTION_OUTBOUND</br></br>在数据报数据层和流数据包层中，此条件指定数据包的方向。</br>在流层和 ALE 流建立的层中，此条件指定连接的方向 (例如，本地应用程序启动连接时，入站数据包 FWPM_CONDITION_DIRECTION 设置为 FWP_DIRECTION_OUTBOUND) 。|
|FWPM_CONDITION_INTERFACE_INDEX|网络堆栈枚举的网络接口的索引。|
|FWPM_CONDITION_INTERFACE_TYPE|网络接口的总线类型。|
|FWPM_CONDITION_SUB_INTERFACE_INDEX|由网络堆栈枚举的逻辑网络接口的索引。|
|FWPM_CONDITION_SOURCE_INTERFACE_INDEX|网络堆栈枚举的转发数据包的源网络接口的索引。|
|FWPM_CONDITION_SOURCE_SUB_INTERFACE_INDEX|网络堆栈枚举的转发数据包的源逻辑网络接口的索引。|
|FWPM_CONDITION_DESTINATION_INTERFACE_INDEX|网络堆栈枚举的转发数据包的目标网络接口的索引。|
|FWPM_CONDITION_DESTINATION_SUB_INTERFACE_INDEX|网络堆栈枚举的转发数据包的目标逻辑网络接口的索引。|
|FWPM_CONDITION_ALE_APP_ID|应用程序的完整路径。|
|FWPM_CONDITION_ALE_USER_ID|本地用户的标识。|
|FWPM_CONDITION_ALE_REMOTE_USER_ID|远程用户的标识。|
|FWPM_CONDITION_ALE_REMOTE_MACHINE_ID|远程计算机的标识。|
|FWPM_CONDITION_ALE_PROMISCUOUS_MODE|允许或拒绝的原始套接字模式。 可能的条件值为：</br>-SIO_RCVALL</br>-SIO_RCVALL_IGMPMCAST</br>-SIO_RCVALL_MCAST</br>有关这些原始套接字模式的说明，请参阅 Microsoft Windows SDK 文档中的 [WSAIoctl](/windows/win32/api/winsock2/nf-winsock2-wsaioctl) 。|
|FWPM_CONDITION_ALE_SIO_FIREWALL_SYSTEM_PORT|保留以供内部使用。|
|FWPM_CONDITION_ALE_NAP_CONTEXT|保留以供内部使用。|
|FWPM_CONDITION_REMOTE_USER_TOKEN|远程用户的标识。|
|FWPM_CONDITION_RPC_IF_UUID|RPC 接口的 UUID。|
|FWPM_CONDITION_RPC_IF_VERSION|RPC 接口的版本。|
|FWPM_CONDITION_RCP_IF_FLAG|保留以供内部使用。|
|FWPM_CONDITION_DCOM_APP_ID|COM 应用程序的标识。|
|FWPM_CONDITION_IMAGE_NAME|应用程序的名称。|
|FWPM_CONDITION_RPC_PROTOCOL|RPC 协议。 可能的条件值为：</br>-RPC_PROTSEQ_TCP</br>-RPC_PROTSEQ_HTTP</br>-RPC_PROTSEQ_NMP|
|FWPM_CONDITION_RPC_AUTH_TYPE|身份验证服务类型。 有关身份验证服务类型的详细信息，请参阅 Windows SDK 文档的 RPC 部分中的 [身份验证-服务常量](/windows/desktop/Rpc/authentication-service-constants) 。|
|FWPM_CONDITION_RPC_AUTH_LEVEL|身份验证服务级别。 有关身份验证服务级别的详细信息，请参阅 Windows SDK 文档的 RPC 部分中的 [身份验证级别常量](/windows/desktop/Rpc/authentication-level-constants) 。|
|FWPM_CONDITION_SEC_ENCRYPT_ALGORITHM|基于证书的安全服务提供程序接口 (SSPI) 加密算法。|
|FWPM_CONDITION_SEC_KEY_SIZE|基于证书的安全服务提供程序接口 (SSPI) 加密密钥大小。|
|FWPM_CONDITION_IP_LOCAL_ADDRESS_V4|本地 IPv4 地址。|
|FWPM_CONDITION_IP_LOCAL_ADDRESS_V6|本地 IPv6 地址。|
|FWPM_CONDITION_PIPE|远程命名管道的名称。|
|FWPM_CONDITION_IP_REMOTE_ADDRESS_V4|远程 IPv4 地址。|
|FWPM_CONDITION_IP_REMOTE_ADDRESS_V6|远程 IPv6 地址。|
|FWPM_CONDITION_PROCESS_WITH_RPC_IF_UUID|具有 RPC 接口的进程的 UUID。|
|FWPM_CONDITION_RPC_EP_VALUE|保留以供内部使用。|
|FWPM_CONDITION_RPC_EP_FLAGS|保留以供内部使用。|
|FWPM_CONDITION_CLIENT_TOKEN|使用 RpcProxy 时客户端的标识。|
|FWPM_CONDITION_RPC_SERVER_NAME|RPC 服务器的名称（使用 RpcProxy 时）。|
|FWPM_CONDITION_RPC_SERVER_PORT|使用 RpcProxy 时 RPC 服务器上的端口。|
|FWPM_CONDITION_RPC_PROXY_AUTH_TYPE|RPC 代理身份验证服务类型。 有关身份验证服务类型的详细信息，请参阅 Windows SDK 文档的 RPC 部分中的 [身份验证-服务常量](/windows/desktop/Rpc/authentication-service-constants) 。|
|FWPM_CONDITION_TUNNEL_TYPE|隧道使用的封装方法。|
|FWPM_CONDITION_CLIENT_CERT_KEY_LENGTH|安全套接字层 (SSL) 客户端证书中的密钥长度。|
|FWPM_CONDITION_CLIENT_CERT_OID| (OID) 客户端证书中的对象标识符。|
|FWPM_CONDITION_INTERFACE_MAC_ADDRESS|发送或接收网络接口的物理地址。</br>**注意** 在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_LOCAL_ADDRESS|本地网络接口的物理地址。 对于入站流量，这是帧中的目标 MAC 地址。 对于出站流量，这是帧的源 MAC 地址。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_REMOTE_ADDRESS|远程网络接口的物理地址。 对于入站流量，这是帧中的源 MAC 地址。 对于出站流量，这是帧的目标 MAC 地址。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_ETHER_TYPE|MAC 帧中指示的类型。 对于 IPv4 流量，此值为0x800，对于 IPv6 流量为0x86DD，对于 ARP 流量为0x806。  所有可能的值在 ntddndis 中定义为 NDIS_ETH_TYPE_Xxx。|
|FWPM_CONDITION_VLAN_ID|以太网 SNAP 标头中 VLAN 的标识符。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_NDIS_PORT|标识微型端口适配器端口的端口号。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_NDIS_MEDIA_TYPE|指定为 [NDIS_MEDIUM](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_medium) 枚举值之一的 NDIS 介质的类型。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_NDIS_PHYSICAL_MEDIA_TYPE|指定为 NDIS_PHYSICAL_MEDIUM 枚举值之一的通信接口的物理介质的类型。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_L2_FLAGS|用于 MAC 层的筛选条件标志组合的按位 "或"。 有关可能的标志的信息，请参阅 [筛选条件 L2 标志](filtering-condition-l2-flags.md)。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_LOCAL_ADDRESS_TYPE|本地 MAC 地址的链接类型。 这是在 FwpmTypes 中的 [DL_ADDRESS_TYPE](/windows/win32/api/fwpmtypes/ne-fwpmtypes-dl_address_type) 枚举中定义的值之一。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_REMOTE_ADDRESS_TYPE|远程 MAC 地址的链接类型。 这是在 FwpmTypes 中的 [DL_ADDRESS_TYPE](/windows/win32/api/fwpmtypes/ne-fwpmtypes-dl_address_type) 枚举中定义的值之一。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_INTERFACE|与本地 MAC 地址关联的网络接口的 LUID。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_ALE_PACKAGE_ID|AppContainer 受限包的安全标识符 (SID) 。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_SOURCE_ADDRESS|创建 MAC 帧的网络接口的物理地址。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_DESTINATION_ADDRESS|帧的目标网络接口的物理地址。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_SOURCE_ADDRESS_TYPE|创建该帧的接口的 MAC 地址的链接类型。 这是在 FwpmTypes 中的 [DL_ADDRESS_TYPE](/windows/win32/api/fwpmtypes/ne-fwpmtypes-dl_address_type) 枚举中定义的值之一。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_MAC_DESTINATION_ADDRESS_TYPE|帧的目标接口的 MAC 地址的链接类型。 这是在 FwpmTypes 中的 [DL_ADDRESS_TYPE](/windows/win32/api/fwpmtypes/ne-fwpmtypes-dl_address_type) 枚举中定义的值之一。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_IP_SOURCE_PORT|传输协议源端口号。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_IP_DESTINATION_PORT|传输协议目标端口号。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_ID|虚拟交换机的 GUID。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_NETWORK_TYPE|与虚拟交换机关联的网络的类型。 这是在 FwpTypes 中的 [FWP_VSWITCH_NETWORK_TYPE](/windows/win32/api/fwptypes/ne-fwptypes-fwp_vswitch_network_type) 枚举中定义的值之一。</br>**注意**  在 windows 8 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_ID|创建该帧的虚拟交换机的接口的 GUID。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_ID|帧所指向的虚拟交换机的接口的 GUID。</br>**注意**  在 windows 8 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_SOURCE_INTERFACE_TYPE|创建该帧的虚拟交换机接口的类型。 这是在 Ntddndis 中的 [NDIS_NIC_SWITCH_TYPE](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_nic_switch_type) 枚举中定义的值之一。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_DESTINATION_INTERFACE_TYPE|帧的目标虚拟交换机接口的类型。 这是在 Ntddndis 中的 [NDIS_NIC_SWITCH_TYPE](/windows-hardware/drivers/ddi/ntddndis/ne-ntddndis-_ndis_nic_switch_type) 枚举中定义的值之一。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_SOURCE_VM_ID|VSwitch 源虚拟机的唯一标识符。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_DESTINATION_VM_ID|VSwitch 目标虚拟机的唯一标识符。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_VSWITCH_TENANT_NETWORK_ID|VSwitch 网络的唯一标识符。 不能与 VLAN_IDs 结合使用。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_ALE_PACKAGE_ID|应用容器 (SID) 的安全标识符。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_ALE_ORIGINAL_APP_ID|在从代理更改之前，应用程序的原始完整路径。  请注意，如果不涉及代理，则该代理将与 FWPM_CONDITION_ALE_APP_ID 相同。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
|FWPM_CONDITION_QM_MODE|快速模式 (QM) 模式。</br>**注意**  在 windows 8、Windows Server 2012 和更高版本的 Windows 中受支持。|
