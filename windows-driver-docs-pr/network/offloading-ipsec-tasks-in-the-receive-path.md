---
title: 在接收路径中卸载 IPsec 任务
description: 在接收路径中卸载 IPsec 任务
ms.assetid: d1dff4fa-7354-4c8c-8591-223c6b524619
keywords:
- ESP 受保护的数据包，WDK IPsec 卸载、 接收路径卸载
- AH 受保护的数据包，WDK IPsec 卸载、 接收路径卸载
- 接收路径卸载 WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 173ce6885d4b161f40b93be6f625958a523ac60e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359348"
---
# <a name="offloading-ipsec-tasks-in-the-receive-path"></a>在接收路径中卸载 IPsec 任务

\[IPsec 任务卸载功能已弃用，不应使用。\]




当 NIC 执行 Internet 协议安全 (IPsec) 处理上接收数据包时，它会解密数据包如果数据包包含 ESP 有效负载，并计算 AH 或 ESP 加密校验和 （或两者） 数据包。 之前，该值指示[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388) TCP/IP 传输，微型端口驱动程序调用到数据包结构[ **NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff568401)宏替换 *\_Id*的**IPsecOffloadV1NetBufferListInfo**以获取[ **NDIS\_IPSEC\_卸载\_V1\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565801)结构，它是与包相关联。

微型端口驱动程序集**CryptoDone**标志在 NDIS\_IPSEC\_卸载\_V1\_NET\_缓冲区\_列表\_信息结构若要指示 NIC 执行 IPsec 上接收数据包中的至少一个 IPsec 有效负载的检查。 如果 NIC 执行 IPsec 隧道和传输的接收数据包的各个部分检查，微型端口驱动程序还会设置**NextCryptoDone**标志在 NDIS\_IPSEC\_卸载\_V1\_NET\_缓冲区\_列表\_信息结构。 微型端口驱动程序集**NextCryptoDone**仅当数据包具有隧道和传输 IPsec 负载。 否则，微型端口驱动程序设置**NextCryptoDone**为零。 若要指示 IPsec 检查的结果，微型端口驱动程序还必须提供的值**CryptoStatus**成员在 NDIS\_IPSEC\_卸载\_V1\_NET\_缓冲区\_列表\_信息结构。 如果 NIC 检测到校验和失败或解密失败，微型端口驱动程序必须指明[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)任何形式的接收数据包的结构它是，指定合适**CryptoStatus**值。

请注意，如果微型端口驱动程序不解密的传入数据包，它会清除这两**CryptoDone**并**NextCryptoDone**标志。 微型端口驱动程序自动完成这所有接收数据包不会解密，而不管该数据包是受保护的 AH 或 ESP 受保护。 微型端口驱动程序集**CryptoStatus**加密到\_成功不会解密的所有数据包。

后微型端口驱动程序指示 NET\_缓冲区\_到 TCP/IP 传输，传输的列表结构检查的执行，NIC 检查数据包的序列号的 IPsec 检查结果，并确定什么若要使用的数据包，校验和或序列化测试失败执行操作。

 

 





