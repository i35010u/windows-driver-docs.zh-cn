---
title: 停止驱动程序堆栈
description: 停止驱动程序堆栈
ms.assetid: 2ecc0ebb-89d8-4cd8-ac1c-f9f1da7d2ca8
keywords:
- 驱动程序堆栈 WDK 网络停止
- 正在停止驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e897216b548b996cdd5b1a2c3fa5d714b868903
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366476"
---
# <a name="stopping-a-driver-stack"></a>停止驱动程序堆栈





如果移除某个设备，NDIS 停止驱动程序堆栈。 驱动程序堆栈停止操作继续进行，如下所示：

1.  NDIS 暂停驱动程序堆栈。 有关暂停的驱动程序堆栈的详细信息，请参阅[暂停驱动程序堆栈](pausing-a-driver-stack.md)。

2.  NDIS 调用协议驱动程序[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数。

    该绑定会进入关闭状态。 未完成的 OID 和发送请求已完成，所有接收后返回数据，该绑定将进入未绑定状态。

3.  NDIS 分离所有筛选器模块，从堆栈顶部开始并向微型端口驱动程序的进展情况。

    NDIS 调用筛选器驱动程序的后[ *FilterDetach* ](https://msdn.microsoft.com/library/windows/hardware/ff549918)函数和筛选器驱动程序版本中的筛选器模块的所有资源、 筛选器模块处于已分离状态。

4.  NDIS 停止微型端口适配器。

    NDIS 调用微型端口驱动程序的后[ *MiniportHaltEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559388)函数，微型端口驱动程序释放所有资源的微型端口适配器和微型端口适配器处于暂停状态。

5.  如果分离所有筛选器驱动程序的模块，系统可以卸载该筛选器驱动程序。

6.  如果所有的微型端口驱动程序管理的微型端口适配器都将暂停，系统可以卸载微型端口驱动程序。

 

 





