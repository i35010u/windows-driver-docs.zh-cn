---
title: 在接收路径中卸载 IPsec 任务
description: 在接收路径中卸载 IPsec 任务
ms.assetid: d1dff4fa-7354-4c8c-8591-223c6b524619
keywords:
- 受 ESP 保护的数据包 WDK IPsec 卸载，接收路径卸载
- 受 AH 保护的数据包 WDK IPsec 卸载，接收路径卸载
- 接收路径卸载 WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24bcb84fbd67fdf61f255fb8dbde9c5d220d4065
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834634"
---
# <a name="offloading-ipsec-tasks-in-the-receive-path"></a>在接收路径中卸载 IPsec 任务

\[IPsec 任务卸载功能已弃用，不应使用。\]




当 NIC 对接收数据包执行 Internet 协议安全性（IPsec）处理时，如果数据包包含 ESP 有效负载并为数据包计算 AH 或 ESP 加密校验和，则会解密数据包。 在将数据包的[**net\_buffer\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构设置为 tcp/ip 传输之前，微型端口驱动程序会调用[**NET\_缓冲区\_列表\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-info)宏，其 *\_Id*为**IPsecOffloadV1NetBufferListInfo**获取[**NDIS\_IPSEC\_卸载\_V1\_NET\_BUFFER\_列出**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)与数据包关联\_INFO 结构。

微型端口驱动程序在 NDIS 中设置**CryptoDone**标志\_IPSEC\_卸载\_V1\_NET\_BUFFER\_LIST\_INFO 结构，以指示 NIC 至少执行了一个 ipsec 负载检查在接收数据包中。 如果 NIC 同时对接收数据包的隧道和传输部分执行 IPsec 检查，则微型端口驱动程序还会将 NDIS 中的**NextCryptoDone**标志设置\_IPSEC\_卸载\_V1\_NET\_BUFFER\_列表\_信息结构。 仅当数据包同时具有隧道和传输 IPsec 负载时，微型端口驱动程序才会设置**NextCryptoDone** 。 否则，微型端口驱动程序将**NextCryptoDone**设置为零。 为指示 IPsec 检查的结果，微型端口驱动程序还必须为 NDIS 中的**CryptoStatus**成员提供一个值\_IPSEC\_卸载\_V1\_NET\_\_\_INFO 结构。 如果 NIC 检测到校验和失败或解密失败，则微型端口驱动程序必须以任何形式为接收数据包指定一个[**网络\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构，并指定相应的**CryptoStatus**值。

请注意，如果微型端口驱动程序未解密传入数据包，则会清除**CryptoDone**和**NextCryptoDone**标志。 微型端口驱动程序对其不解密的所有接收数据包执行此项，而不考虑数据包是受 AH 保护的还是受 ESP 保护的。 微型端口驱动程序将**CryptoStatus**设置为对其不解密的所有数据包执行加密\_成功。

在微型端口驱动程序指示网络\_缓冲区\_列表结构到 TCP/IP 传输的情况下，传输检查 NIC 执行的 IPsec 检查的结果，检查数据包的序列号，并确定如何处理无法通过校验和或顺序测试的数据包。

 

 





