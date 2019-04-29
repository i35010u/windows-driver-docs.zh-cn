---
title: NDIS 端口发送和接收操作
description: NDIS 端口发送和接收操作
ms.assetid: f9a22b7b-5565-4d56-a9b9-22562b6bf0da
keywords:
- 端口 WDK NDIS 发送和接收操作
- NDIS 端口 WDK、 发送和接收操作
- 将操作 WDK NDIS 发送端口
- 接收操作 WDK NDIS 端口
- 目标端口 WDK NDIS
- 源端口 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3a1cff504824aa5e1796f0dbb196fe41fd05e3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378286"
---
# <a name="ndis-port-send-and-receive-operations"></a>NDIS 端口发送和接收操作





NDIS 驱动程序可以将相关联的发送和接收使用 NDIS 端口的操作。中的端口号*PortNumber*参数 NDIS 发送和接收函数标识发送操作的目标端口或接收指示的源端口。 如果*PortNumber*为零，将使用默认端口。 当 NDIS 处理的默认端口和微型端口驱动程序不会分配任何其他端口时，驱动程序堆栈中的没有 NDIS 驱动程序所需执行任何操作超出总是设置*PortNumber*参数为零。 有关分配微型端口驱动程序中的端口的详细信息，请参阅[Allocating NDIS 端口](allocating-an-ndis-port.md)。

如果微型端口驱动程序分配端口，过量驱动程序可以使用这些端口来发送和接收相关联的微型端口适配器的相应子接口上的数据。 但是，基础驱动程序必须确保端口发送的任何数据之前处于活动状态。 在关联的子接口变得可用时，微型端口驱动程序将激活端口。 有关激活微型端口驱动程序中的端口的详细信息，请参阅[激活 NDIS 端口](activating-an-ndis-port.md)。

当调用 NDIS [ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)协议驱动程序，NDIS 函数提供了一系列中的所有当前活动端口**ActivePorts** 的成员[**NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)结构*BindParameters*参数指向。 NDIS 还会通知与即插即用事件时端口是激活和停用协议驱动程序。 有关即插即用端口的激活和停用通知的详细信息，请参阅[处理 NDIS 端口即插即用通知](handling-ndis-ports-pnp-event-notifications.md)。 有关更多常规信息大约发送和接收操作，请参阅[发送和接收操作](send-and-receive-operations.md)。

 

 





