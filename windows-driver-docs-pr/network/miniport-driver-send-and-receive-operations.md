---
title: 微型端口驱动程序发送和接收操作
description: 微型端口驱动程序发送和接收操作
ms.assetid: f495cf1f-9896-4259-b885-cff4a0112d17
keywords:
- 微型端口驱动程序 WDK 网络发送数据
- NDIS 微型端口驱动程序 WDK、 发送数据
- 微型端口驱动程序 WDK 网络接收数据
- NDIS 微型端口驱动程序 WDK，接收数据
- 发送数据 WDK 网络
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c92a3629e8be996726811e4479b4fab22098d58a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357257"
---
# <a name="miniport-driver-send-and-receive-operations"></a>微型端口驱动程序发送和接收操作





句柄从过量驱动程序发送请求，并发起的微型端口驱动程序收到的指示。 在单个函数调用，NDIS 微型端口驱动程序可以与多个接收指示链接的列表[ **NET\_缓冲区\_列表**](https://msdn.microsoft.com/library/windows/hardware/ff568388)结构。 微型端口驱动程序可以处理多个网络的列表的发送请求\_缓冲区\_与多个列表结构[ **NET\_缓冲区**](https://msdn.microsoft.com/library/windows/hardware/ff568376)上每个网络的结构\_缓冲区\_列表结构。

微型端口驱动程序必须管理接收的缓冲池。 大多数微型端口驱动程序创建的预分配单个 NET 应用程序池\_缓冲区结构与每个 NET\_缓冲区\_列表结构。

以下主题提供有关微型端口驱动程序缓冲区管理的详细信息，发送操作，并接收操作：

[微型端口驱动程序缓冲区管理](miniport-driver-buffer-management.md)

[从微型端口驱动程序发送数据](sending-data-from-a-miniport-driver.md)

[正在取消微型端口驱动程序中的发送请求](canceling-a-send-request-in-a-miniport-driver.md)

[指示从微型端口驱动程序收到的数据](indicating-received-data-from-a-miniport-driver.md)

 

 





