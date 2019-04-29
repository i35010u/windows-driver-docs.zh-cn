---
title: 在发送路径中卸载 IPsec 任务
description: 在发送路径中卸载 IPsec 任务
ms.assetid: b95878e0-0aee-43cb-a64c-b5d8e07cb1b4
keywords:
- WDK IPsec 卸载、 受保护的 ESP 数据包发送路径卸载
- WDK IPsec 卸载、 受保护的 AH 数据包发送路径卸载
- 发送路径卸载 WDK IPsec 卸载
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ced113f09c7b91db094da2e954446eb31753e777
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359342"
---
# <a name="offloading-ipsec-tasks-in-the-send-path"></a>在发送路径中卸载 IPsec 任务

\[IPsec 任务卸载功能已弃用，不应使用。\]




TCP/IP 传输将传递给微型端口驱动程序之前[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388) NIC 将其执行 Internet 协议安全性 (IPsec) 的数据包的结构任务，将更新与网络相关联的 IPsec 信息\_缓冲区\_列表结构。 TCP/IP 传输指定此信息[ **NDIS\_IPSEC\_卸载\_V1\_NET\_缓冲区\_列表\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff565801)结构，它是网络的一部分\_缓冲区\_与网络相关联的列表信息 （带外数据）\_缓冲区\_列表结构。

TCP/IP 传输提供*OffloadHandle*，它指定的句柄发送数据包的传输 （端到端连接） 部分的出站 SA。 如果将通过隧道传输该数据包，还提供了 TCP/IP 传输*NextOffloadHandle*，它指定的句柄发送数据包的隧道部分的出站 SA。

后微型端口驱动程序收到[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构中其[ *MiniportSendNetBufferLists*](https://msdn.microsoft.com/library/windows/hardware/ff559440)或[ **MiniportCoSendNetBufferLists** ](https://msdn.microsoft.com/library/windows/hardware/ff559365)函数，它可以调用[ **NET\_缓冲区\_列表\_INFO** ](https://msdn.microsoft.com/library/windows/hardware/ff568401)宏替换 *\_Id*的**IPsecOffloadV1NetBufferListInfo**获取 NDIS\_IPSEC\_将卸载\_V1\_NET\_缓冲区\_列表\_与网络相关联的信息结构\_缓冲区\_列表结构。

当 NIC 执行 IPsec 上发送数据包的处理时，它为数据包计算 AH 或 ESP 加密校验和 （或两者），并且如果数据包中包含的 ESP 负载，加密数据包。 TCP/IP 传输已构建框架数据包、 填充它 （如果有必要），并为其分配序列号和 SPI。

 

 





