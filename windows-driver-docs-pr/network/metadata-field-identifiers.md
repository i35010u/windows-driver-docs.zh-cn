---
title: 元数据字段标识符
description: 本部分介绍 Windows 筛选平台标注驱动程序的元数据字段标识符。
ms.assetid: 2157bace-9fae-41e8-a435-c4a412873ee1
keywords:
- 元数据字段标识符网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b147a2fbe45e8c064735275b84b447d1046c2b6
ms.sourcegitcommit: 62c81d88b03bd311d1cdfef5b138d579faceb304
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2020
ms.locfileid: "92113504"
---
# <a name="metadata-field-identifiers"></a>元数据字段标识符

每个元数据字段标识符由一个位域表示。 这些标识符定义如下：

|元数据字段标识符|说明|
|--- |--- |
|FWPS_METADATA_FIELD_ALE_CLASSIFY_REQUIRED|入站数据包也会向 FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4 和 FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6 筛选层进行指示。 **注意：**   Windows Server 2008、Windows Vista Service Pack 1 (SP1) 和更高版本中受支持。|
|FWPS_METADATA_FIELD_COMPARTMENT_ID|接收或发送数据包的路由隔离舱的标识符。|
|FWPS_METADATA_FIELD_COMPLETION_HANDLE|用于挂起当前筛选操作的完成句柄。|
|FWPS_METADATA_FIELD_DESTINATION_INTERFACE_INDEX|要在其中发送传出数据包的网络接口的索引。|
|FWPS_METADATA_FIELD_DESTINATION_PREFIX|传出数据包的目标 IPV4 或 IPV6 地址和子网掩码。 **注意：**   支持从 Windows 7 开始。|
|FWPS_METADATA_FIELD_DISCARD_REASON|丢弃数据的原因。|
|FWPS_METADATA_FIELD_ETHER_FRAME_LENGTH|此元数据字段标识符当前不受支持。|
|FWPS_METADATA_FIELD_FLOW_HANDLE|数据流的句柄。|
|FWPS_METADATA_FIELD_FORWARD_LAYER_INBOUND_PASS_THRU|遍历 FWPM_LAYER_IPFORWARD_V4 或 FWPM_LAYER_IPFORWARD_V6 转发层的数据包在本地 (其目标匹配分配给主机) 接口的地址。 **注意：**   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。|
|FWPS_METADATA_FIELD_FORWARD_LAYER_OUTBOUND_PASS_THRU|遍历 FWPM_LAYER_IPFORWARD_V4 或 FWPM_LAYER_IPFORWARD_V6 转发层的数据包在本地生成。 **注意：**   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。|
|FWPS_METADATA_FIELD_FRAGMENT_DATA|接收的数据包片段的片段数据。|
|FWPS_METADATA_FIELD_ICMP_ID_AND_SEQUENCE|ICMP 回送请求或回显答复数据包的标识符和序列号字段。 **注意：**   支持从 Windows 7 开始。|
|FWPS_METADATA_FIELD_IP_HEADER_SIZE|IP 标头的大小。|
|FWPS_METADATA_FIELD_LOCAL_REDIRECT_TARGET_PID|连接已重定向到的进程 ID。 **注意：**   支持从 Windows 7 开始。|
|FWPS_METADATA_FIELD_ORIGINAL_DESTINATION|一个 [**SOCKADDR_STORAGE**](/previous-versions/windows/desktop/legacy/ms740504(v=vs.85)) 结构，指示数据包的原始目标。 **注意：**   支持从 Windows 7 开始。|
|FWPS_METADATA_FIELD_PACKET_DIRECTION|网络流量 (入站或出站) 的方向。|
|FWPS_METADATA_FIELD_PACKET_SYSTEM_CRITICAL|预留给系统使用。 请勿使用。 **注意：**   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。|
|FWPS_METADATA_FIELD_PARENT_ENDPOINT_HANDLE|终结点的父套接字的句柄。 **注意：**   支持从 Windows 7 开始。|
|FWPS_METADATA_FIELD_PATH_MTU|传出数据包 (路径 MTU) 路径最大传输单元。|
|FWPS_METADATA_FIELD_PROCESS_ID|拥有终结点的进程的进程 ID。|
|FWPS_METADATA_FIELD_PROCESS_PATH|拥有终结点的进程的完整路径。|
|FWPS_METADATA_FIELD_REDIRECT_RECORD_HANDLE|"重定向记录" 句柄由分类元数据指定 ALE_CONNECT_REDIRECT 标注。 **注意：**   从 Windows 8 开始支持。|
|FWPS_METADATA_FIELD_REMOTE_SCOPE_ID|要用于出站传输层注入的远程作用域标识符。|
|FWPS_METADATA_FIELD_RESERVED|预留给系统使用。 请勿使用。|
|FWPS_METADATA_FIELD_SOURCE_INTERFACE_INDEX|接收传入数据包的网络接口的索引。|
|FWPS_METADATA_FIELD_SUB_PROCESS_TAG|预留给系统使用。|
|FWPS_METADATA_FIELD_SYSTEM_FLAGS|筛选器引擎在内部使用的系统标志。|
|FWPS_METADATA_FIELD_TOKEN|用于验证用户的权限的令牌。|
|FWPS_METADATA_FIELD_TRANSPORT_CONTROL_DATA|可选套接字控件数据对象。|
|FWPS_METADATA_FIELD_TRANSPORT_ENDPOINT_HANDLE|要注入到出站传输层的数据包末尾的句柄。|
|FWPS_METADATA_FIELD_TRANSPORT_HEADER_INCLUDE_HEADER|如果数据包是从原始套接字发送的，则为 IP 标头。 **注意：**   在 Windows Server 2008、Windows Vista SP1 和更高版本中受支持。|
|FWPS_METADATA_FIELD_TRANSPORT_HEADER_SIZE|传输标头的大小。|
