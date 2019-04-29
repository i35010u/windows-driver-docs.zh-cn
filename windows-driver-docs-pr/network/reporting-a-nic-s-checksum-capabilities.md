---
title: 报告 NIC 的校验和功能
description: 报告 NIC 的校验和功能
ms.assetid: a90f8d01-8318-44de-acf0-7903ef7e85e0
keywords:
- 任务卸载，WDK TCP/IP 传输，校验和任务
- 校验和任务 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a00faa6a5cbe908f075c4fa822ffa2adce92d3de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361819"
---
# <a name="reporting-a-nics-checksum-capabilities"></a>报告 NIC 的校验和功能





NIC 是否当前配置为计算和验证中的 IP、 TCP 和 UDP 校验和 NDIS 微型端口驱动程序报告[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567878)结构。 微型端口驱动程序必须包括中的当前校验和卸载配置[ **NDIS\_微型端口\_适配器\_卸载\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)结构。 微型端口驱动程序调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)函数从[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数并传递中信息在 NDIS\_微型端口\_适配器\_卸载\_属性。

微型端口驱动程序必须报告当前校验和卸载配置中的更改，如果有，请在[ **NDIS\_状态\_任务\_卸载\_当前\_配置** ](https://msdn.microsoft.com/library/windows/hardware/ff567424)状态指示。

中的查询响应[OID\_TCP\_卸载\_当前\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)，NDIS 包括 NDIS\_TCP\_IP\_的校验和\_在卸载结构[ **NDIS\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS 返回中的结构**InformationBuffer**隶属[**NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。 NDIS 使用微型端口驱动程序提供的信息。

微型端口驱动程序获取 IPv4 和 IPv6 发送和接收数据包的指示以下的校验和信息：

-   类型的校验和 （IP、 TCP 或 UDP），NIC 可以计算为发送数据包，并可以验证为接收数据包。

-   封装设置，请在**封装**成员。 有关此成员的详细信息，请参阅中的备注部分[ **NDIS\_TCP\_IP\_校验和\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff567878)。

-   NIC 可以计算或验证 （或计算并验证） 数据包的校验和是否其 IP 标头将包含 IPv4 选项。

-   NIC 可以计算或验证 （或计算并验证） 的 IPv6 数据包校验和是否其 IP 标头将包含 IPv6 扩展标头。

-   NIC 可以计算或验证 （或计算并验证） 数据包的校验和是否其 TCP 报头包含 TCP 选项。

## <a name="related-topics"></a>相关主题


[确定任务卸载功能](determining-task-offload-capabilities.md)

 

 






