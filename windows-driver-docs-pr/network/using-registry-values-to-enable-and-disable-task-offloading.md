---
title: 使用注册表值启用和禁用任务卸载
description: 使用注册表值启用和禁用任务卸载
keywords:
- 任务卸载 WDK TCP/IP 传输，注册表值
- 注册表 WDK TCP/IP 卸载
- 任务卸载 WDK TCP/IP 传输，启用服务
- 任务卸载 WDK TCP/IP 传输，禁用服务
ms.date: 10/30/2020
ms.localizationpriority: medium
ms.custom: contperfq2
ms.openlocfilehash: d661c1edce72e9205af0196dc2d5db24f5176eee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839415"
---
# <a name="using-registry-values-to-enable-and-disable-task-offloading"></a>使用注册表值启用和禁用任务卸载





调试驱动程序的任务卸载功能时，您可能会发现使用注册表项设置启用或禁用任务卸载服务很有用。 你可以在 INF 文件和注册表中定义标准化关键字。 有关标准化关键字的详细信息，请参阅 [网络设备的标准化 INF 关键字](standardized-inf-keywords-for-network-devices.md)。

任务卸载关键字属于以下两个组之一：粒度关键字或分组关键字。 *精细关键字* 提供每个卸载功能的关键字--传输层差异、IP 协议差异。 *分组关键字* 在传输层提供组合关键字功能。

## <a name="granular-keywords"></a>细粒度关键字

精细关键字定义如下：

|关键字|描述|
|--- |--- |
|**\*IPChecksumOffloadIPv4**|描述设备是启用还是禁用了 IPv4 校验和的计算。|
|**\*TCPChecksumOffloadIPv4**|描述设备是启用还是禁用了对 IPv4 数据包的 TCP 校验和的计算。|
|**\*TCPChecksumOffloadIPv6**|描述设备是启用还是禁用了对 IPv6 数据包的 TCP 校验和的计算。|
|**\*UDPChecksumOffloadIPv4**|描述设备是启用还是禁用了对 IPv4 数据包的 UDP 校验和的计算。|
|**\*UDPChecksumOffloadIPv6**|描述设备是启用还是禁用了对 IPv6 数据包的 UDP 校验和的计算。|
|**\*LsoV1IPv4**|描述设备是启用还是禁用了在大型发送卸载版本 1 (LSOv1) 的情况上对大型 TCP 数据包的分段。|
|**\*LsoV2IPv4**|描述设备是启用还是禁用了在大型发送卸载版本 2 (LSOv2) 的情况通过 IPv4 对大 TCP 数据包的分段。|
|**\*LsoV2IPv6**|描述设备是启用还是禁用了通过 IPv6 将大 TCP 数据包分段用于大规模发送卸载版本 2 (LSOv2) 。|
|**\*IPsecOffloadV1IPv4** |描述设备是启用还是禁用了通过 IPv4 计算 IPsec 标头。|
|**\*IPsecOffloadV2** |介绍设备启用还是禁用 IPsec 卸载版本 2 (IPsecOV2) 。 IPsecOV2 提供了对大量发送卸载版本 2 (LSOv2) 的其他加密算法、IPv6 和共存支持。|
|**\*IPsecOffloadV2IPv4**  |描述设备是启用还是禁用 IPsecOV2 仅适用于 IPv4。|

下表描述了可用于配置卸载服务的精细关键字。

|SubkeyName|ParamDesc|“值”|EnumDesc|
|--- |--- |--- |--- |
|**_IPChecksumOffloadIPv4_**|IPv4 校验和卸载|0|已禁用|
|||1|已启用 Tx|
|||2|已启用 Rx|
|||3 (默认值) |Rx & Tx 已启用|
|**TCPChecksumOffloadIPv4**|TCP 校验和卸载 (IPv4) |0|已禁用|
|||1|已启用 Tx|
|||2|已启用 Rx|
|||3 (默认值) |Rx & Tx 已启用|
|**_TCPChecksumOffloadIPv6_**|TCP 校验和卸载 (IPv6) |0|已禁用|
|||1|已启用 Tx|
|||2|已启用 Rx|
|||3 (默认值) |Rx & Tx 已启用|
|**UDPChecksumOffloadIPv4**|UDP 校验和卸载 (IPv4) |0|已禁用|
|||1|已启用 Tx|
|||2|已启用 Rx|
|||3 (默认值) |Rx & Tx 已启用|
|**_UDPChecksumOffloadIPv6_**|UDP 校验和卸载 (IPv6) |0|已禁用|
|||1|已启用 Tx|
|||2|已启用 Rx|
|||3 (默认值) |Rx & Tx 已启用|
|**LsoV1IPv4**|大型发送卸载版本 1 (IPv4) |0|已禁用|
|||1 (默认值) |已启用|
|**_LsoV2IPv4_**|大型发送卸载 V2 (IPv4) |0|已禁用|
|||1 (默认值) |已启用|
|**LsoV2IPv6**|大型发送卸载 V2 (IPv6) |0|已禁用|
|||1 (默认值) |已启用|
|**_IPsecOffloadV1IPv4_**|IPsec 卸载版本 1 (IPv4) |0|已禁用|
|||1|已启用身份验证标头|
|||2|已启用 ESP|
|||3 (默认值) |身份验证标头已启用 & ESP|
|**IPsecOffloadV2**|IPsec 卸载|0|已禁用|
|||1|已启用身份验证标头|
|||2|已启用 ESP|
|||3 (默认值) |身份验证标头已启用 & ESP|
|**_IPsecOffloadV2IPv4_*|IPsec 卸载 (仅 IPv4) |0|已禁用|
|||1|已启用身份验证标头|
|||2|已启用 ESP|
|||3 (默认值) |身份验证标头已启用 & ESP|

 

> [!NOTE]
> INF 文件可以支持在 UI 的 "高级" 属性页中显示的精细关键字。 小型端口驱动程序必须在初始化时读取注册表中的所有精细设置，包括未显示的设置，以注册 NDIS 卸载功能。

## <a name="grouped-keywords"></a>分组关键字

按如下所示定义分组关键字：

|关键字|描述|
|--- |--- |
|**\*TCPUDPChecksumOffloadIPv4**|描述设备是启用还是禁用通过 IPv4 计算 IP、TCP 和 UDP 校验和。|
|**\*TCPUDPChecksumOffloadIPv6**|描述设备是启用还是禁用了对 IPv6 的 TCP 和 UDP 校验和的计算。|


下表描述了可用于配置卸载服务的分组关键字。

|SubkeyName|ParamDesc|“值”|EnumDesc|
|--- |--- |--- |--- |
|**_TCPUDPChecksumOffloadIPv4_**|TCP/UDP 校验和卸载 (IPv4) |0|已禁用|
|||1|已启用 Tx|
|||2|已启用 Rx|
|||3 (默认值) |Tx & Rx 已启用|
|**TCPUDPChecksumOffloadIPv6**|TCP/UDP 校验和卸载 (IPv6) |0|已禁用|
|||1|已启用 Tx|
|||2|已启用 Rx|
|||3 (默认值) |Tx & Rx 已启用|
 

可以启用的卸载的组合有限制。 例如，如果微型端口适配器支持 LSOV1 或 LSOV2，则微型端口适配器还会计算 IP 和 TCP 校验和。 有关卸载的有效组合的详细信息，请参阅 [合并类型的任务卸载](combining-types-of-task-offloads.md)。

如果使用注册表项设置禁用了任务卸载服务，则协议驱动程序不得)  (OID 发出 [oid \_ 卸载 \_ 封装](./oid-offload-encapsulation.md) 对象标识符。

你可以使用以下注册表值来启用或禁用 TCP/IP 协议的任务卸载：

<a href="" id="hkey-local-machine-system-currentcontrolset-services-tcpip-parameters-disabletaskoffload-------"></a>**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ 服务 \\ TCPIP \\ 参数 \\ DisableTaskOffload**   
将此值设置为 one 将禁用 TCP/IP 传输中的所有任务卸载。 如果将此值设置为零，则将启用所有任务卸载。

<a href="" id="hkey-local-machine-system-currentcontrolset-services-ipsec-enabledoffload-------"></a>**HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ Ipsec \\ EnabledOffload**   
如果将此值设置为零，则将禁用从 TCP/IP 传输 (IPsec) 卸载的 Internet 协议安全性。 卸载 TCP/IP 校验和任务、大型发送卸载版本 1 (LSOV1) ，以及大量发送卸载版本 2 (LSOV2) 不受影响。 将此值设置为 one 会启用 IPsec 卸载。

 

