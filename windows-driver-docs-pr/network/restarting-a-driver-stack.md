---
title: 重启驱动程序堆栈
description: 重启驱动程序堆栈
ms.assetid: 5c9138f8-4a29-4740-b085-efe24d950fba
keywords:
- 驱动程序堆栈 WDK 连接网络、 重新启动
- 重新启动驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c69bed1aa124a6f777eb7e66108593d2b53939cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391632"
---
# <a name="restarting-a-driver-stack"></a>重启驱动程序堆栈





NDIS 筛选器模块插入或添加一个绑定等操作后重新启动驱动程序堆栈。 驱动程序堆栈的重新启动操作继续进行，如下所示：

1.  NDIS 微型端口适配器将重新启动。

    NDIS 调用微型端口驱动程序的后[ **MiniportRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff559435)函数，微型端口适配器进入正在重新启动状态。 微型端口驱动程序准备继续发送和接收操作。 如果所做的准备失败，微型端口适配器返回到暂停状态。 该驱动程序已准备好继续发送和接收操作后，微型端口适配器进入运行状态。

2.  NDIS 重新启动筛选器模块中，在驱动程序堆栈的底部开始以及最多协议驱动程序的进展情况。

    NDIS 调用筛选器驱动程序的后[ **FilterRestart** ](https://msdn.microsoft.com/library/windows/hardware/ff549962)函数，筛选器模块进入正在重新启动状态。 筛选器驱动程序准备继续发送和接收操作。 如果所做的准备失败，模块将返回到暂停状态。 该驱动程序已准备好继续发送和接收操作后，筛选器模块将进入运行状态。

3.  NDIS 将即插即用的重新启动事件发送到协议驱动程序。

    该绑定将进入正在重新启动状态。 协议驱动程序准备继续发送和接收操作。 如果所做的准备失败，绑定将返回到暂停状态。 协议驱动程序已准备好继续发送和接收操作后，该绑定将进入运行状态。

 

 





