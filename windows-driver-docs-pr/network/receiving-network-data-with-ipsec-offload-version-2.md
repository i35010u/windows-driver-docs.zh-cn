---
title: 使用 IPsec 卸载版本 2 接收网络数据
description: 使用 IPsec 卸载版本 2 接收网络数据
ms.assetid: c09ce374-6dd6-4d16-914b-5576304d4440
keywords:
- IPsecOV2 WDK TCP/IP 传输，接收数据
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6957adc41167e3faf66c39b230c797851c094d1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523217"
---
# <a name="receiving-network-data-with-ipsec-offload-version-2"></a>使用 IPsec 卸载版本 2 接收网络数据

\[IPsec 任务卸载功能已弃用，不应使用。\]




NIC 执行 IPsec 卸载版本 2 (IPsecOV2) 上接收数据包从传输已卸载安全关联 (SA) 中指定的处理。

微型端口驱动程序设置之前，该值指示基础驱动程序所接收的数据的 IPsecOV2 带外 (OOB) 信息。 有关访问 OOB 信息的详细信息，请参阅[访问 NET\_缓冲区\_IPsec 卸载版本 2 中的列表信息](accessing-net-buffer-list-information-in-ipsec-offload-version-2.md)。

**请注意**  微型端口驱动程序应指示接收的所有数据包到过量驱动程序，即使在处理中 NIC 的 IPsec 数据时发生错误 该驱动程序必须指示有错误，若要启用驱动程序堆栈进行监视和故障排除的网络流量的数据包。

 

之前的微型端口驱动程序指示驱动程序堆栈，微型端口驱动程序收到的数据数据包：

-   验证硬件配置为处理 IPsec 卸载任务。 如果不是，微型端口驱动程序不与任何其他 IPsec 的接收指示将处理卸载。

-   查看安全参数索引 (SPI) 以确定是否匹配卸载 SA 存在。 微型端口驱动程序确定数据包的目标地址是与一个指定在卸载的 SA 相同。 如果没有匹配的 SA，NIC 而无需设置 IPsecOV2 OOB 信息指示接收到的数据。

-   确认它可以处理数据包的微型端口驱动程序报告到传输的功能，或者使而无需进一步 IPsec 处理的接收指示。 例如，数据包可能具有其中 NIC 不支持 IPsec 卸载处理此类数据包和微型端口驱动程序执行 IPsec 处理 IP 选项。

-   集**CryptoDone**中的标志[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565818)结构，以指示 NIC 执行 IPsec 检查所接收的数据包中的至少一个 IPsec 有效负载。

-   集**NextCryptoDone**标志在 NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_信息结构，以指示一个 NIC 将执行 IPsec 隧道和传输的接收数据包的各个部分检查。 微型端口驱动程序设置了此标志仅当数据包具有隧道和传输负载;否则，此标志应为零。

-   设置正确**CryptoStatus**值的 NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_信息结构指示 IPsec 检查的结果。

如果 NIC 未执行处理的传入数据包的卸载，微型端口驱动程序将清除这两**CryptoDone**并**NextCryptoDone**标志。 微型端口驱动程序清除这些标志的所有接收其中一个 NIC 不会解密，而不管该数据包是受保护的 AH 或 ESP 受保护的数据包。

微型端口驱动程序可以设置**SaDeleteReq**，在[ **NDIS\_IPSEC\_卸载\_V2\_NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565818)结构的接收[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)。 TCP/IP 传输随后发出[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](https://msdn.microsoft.com/library/windows/hardware/ff569813)一次删除入站上接收数据包的 SA，一次试删除对应于已删除的出站 SA 的入站 SA。 有关添加和删除 SAs 的详细信息，请参阅[IPsec 卸载版本 2 中管理安全关联](managing-security-associations-in-ipsec-offload-version-2.md)。

后微型端口驱动程序指示 NET\_缓冲区\_到 TCP/IP 传输，TCP/IP 传输列表结构检查 IPsec 检查 NIC 上数据包，执行序列号的数据包，检查结果并确定应如何处理的数据包，校验和或序列化测试将失败。

 

 





