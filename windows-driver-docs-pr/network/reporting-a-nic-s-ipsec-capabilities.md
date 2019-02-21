---
title: 报告 NIC 的 IPsec 功能
description: 报告 NIC 的 IPsec 功能
ms.assetid: 6ed02d4a-9b5e-4245-a3f9-f0b5fc8366a7
keywords:
- 任务将 WDK TCP/IP 传输、 IPsec 任务卸载
- IPsec 卸载 WDK TCP/IP 传输，功能
- IPsec 卸载 WDK TCP/IP 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb715f1e9e3b01cc9ec53099807a835e28259707
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555712"
---
# <a name="reporting-a-nics-ipsec-capabilities"></a>报告 NIC 的 IPsec 功能

\[IPsec 任务卸载功能已弃用，不应使用。\]




NDIS 微型端口驱动程序指定的当前 Internet 协议安全 (IPsec) 卸载配置中的 NIC [ **NDIS\_IPSEC\_卸载\_V1** ](https://msdn.microsoft.com/library/windows/hardware/ff565796)结构。微型端口驱动程序必须包含在当前的 IPsec 卸载配置[ **NDIS\_微型端口\_适配器\_卸载\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数从[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数并传递中信息在 NDIS\_微型端口\_适配器\_卸载\_属性。

微型端口驱动程序必须报告更改 ipsec 卸载功能，如果有的话，在[ **NDIS\_状态\_任务\_卸载\_当前\_配置**](https://msdn.microsoft.com/library/windows/hardware/ff567424)状态指示。

中的查询响应[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)，NDIS 包括 NDIS\_IPSEC\_卸载\_V1结构中[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS 返回中的结构**InformationBuffer**隶属[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 NDIS 使用微型端口驱动程序提供的信息。

微型端口驱动程序指示以下信息在 NDIS\_IPSEC\_卸载\_V1 结构：

-   封装设置，请在**封装**成员。 有关此成员的详细信息，请参阅中的备注部分[ **NDIS\_IPSEC\_卸载\_V1**](https://msdn.microsoft.com/library/windows/hardware/ff565796)。

-   NIC 是否可以执行合并 IPsec 数据包-上的操作，即是否 NIC 可以处理的数据包，包含身份验证标头 (AH) 和中使用以下格式的数据包的封装安全负载 (ESP):

    \[IP\]\[AH\]\[ESP\]\[数据包的其余部分\]

-   是否 NIC 可以执行 IP 安全处理的传输模式部分和隧道模式一部分发送和接收数据包。 数据包的传输模式部分适用于一个端到端安全关联，并与隧道安全关联相关的数据包的隧道模式部分。

-   如果数据包的 IP 标头包含的 IP 选项中，NIC 是否可以 IP 上数据包的安全操作。

微型端口驱动程序指定 NIC 来计算或验证 （或计算并验证） 的 AH 有效负载和身份验证信息的加密校验和的以下功能：

-   可以使用 NIC 完整性算法 （MD5 或 SHA 1）

-   是否 NIC 可以处理 AH 安全有效负载：
    -   数据包的传输模式下一部分
    -   数据包隧道模式部分
    -   发送数据包
    -   接收数据包

微型端口驱动程序指定进程 ESP 有效负载的 NIC 的以下功能：

-   可以使用 NIC 保密性算法 （DES、 三重 DES 或两者）

-   NIC 是否支持 null 加密 （即，ESP 有效负载不加密，但使用身份验证哈希）

-   是否 NIC 可以执行 ESP 处理操作：
    -   数据包的传输模式下一部分
    -   数据包隧道模式部分
    -   发送数据包
    -   接收数据包

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






