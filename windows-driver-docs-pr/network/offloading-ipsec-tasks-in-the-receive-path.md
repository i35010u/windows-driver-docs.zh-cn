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
ms.openlocfilehash: bb79e3c200f150215cddf8112a5e7687b19846cd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217531"
---
# <a name="offloading-ipsec-tasks-in-the-receive-path"></a>在接收路径中卸载 IPsec 任务

\[IPsec 任务卸载功能已弃用，不应使用。\]




当 NIC 在接收数据包上执行 Internet 协议安全 (IPsec) 处理时，如果数据包包含 ESP 有效负载，并为数据包 (或) 同时计算 AH 或 ESP 加密校验和，则会解密数据包。 在为 TCP/IP 传输指明包的[**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)结构之前，微型端口驱动程序将使用* \_ Id*为**IPsecOffloadV1NetBufferListInfo**的[**网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_info)宏来获取与数据包关联的[**NDIS \_ IPSEC \_ 卸载 \_ V1 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)结构。

微型端口驱动程序在**CryptoDone** NDIS \_ IPSEC \_ 卸载 \_ V1 \_ 网络缓冲区列表信息结构中设置 CryptoDone 标志， \_ \_ \_ 以指示 NIC 在接收数据包中至少对一个 ipsec 有效负载执行 ipsec 检查。 如果 NIC 对接收数据包的隧道和传输部分执行 IPsec 检查，则微型端口驱动程序还会在 NDIS **NextCryptoDone** \_ IPsec \_ 卸载 \_ V1 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息结构中设置 NextCryptoDone 标志。 仅当数据包同时具有隧道和传输 IPsec 负载时，微型端口驱动程序才会设置 **NextCryptoDone** 。 否则，微型端口驱动程序将 **NextCryptoDone** 设置为零。 为指示 IPsec 检查的结果，微型端口驱动程序还必须为 NDIS **CryptoStatus** \_ IPsec \_ 卸载 \_ V1 \_ NET \_ BUFFER \_ LIST \_ INFO 结构中的 CryptoStatus 成员提供一个值。 如果 NIC 检测到校验和失败或解密失败，则微型端口驱动程序必须以任何形式指示接收数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构，并指定适当的 **CryptoStatus** 值。

请注意，如果微型端口驱动程序未解密传入数据包，则会清除 **CryptoDone** 和 **NextCryptoDone** 标志。 微型端口驱动程序对其不解密的所有接收数据包执行此项，而不考虑数据包是受 AH 保护的还是受 ESP 保护的。 微型端口驱动程序将 **CryptoStatus** 设置为 \_ 不会解密的所有数据包的加密成功。

在微型端口驱动程序指示 \_ tcp/ip 传输的网络缓冲区 \_ 列表结构后，传输将检查 NIC 所执行的 IPsec 检查的结果，检查数据包的序列号，并确定如何处理未通过校验和或顺序测试的数据包。

 

