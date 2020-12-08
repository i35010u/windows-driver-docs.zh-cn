---
title: 增强的运行时重新配置功能
description: 增强的运行时重新配置功能
keywords:
- 驱动程序堆栈 WDK 网络，暂停
- 驱动程序堆栈 WDK 网络，重新启动
- 暂停驱动程序堆栈 WDK 网络
- 重新启动驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86e7e246d9f12c4511a8677f6b8aad2425515450
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823935"
---
# <a name="enhanced-run-time-reconfiguration-abilities"></a>增强的运行时重新配置功能





NDIS 6.0 引入了暂停和重新启动驱动程序堆栈的功能，而无需关闭堆栈并构建一个新堆栈。 所有 NDIS 6.0 和更高版本的驱动程序都必须支持暂停和重启服务。

暂停堆栈可消除同步问题，因为在进行重新配置之前，所有驱动程序都处于已知状态。 暂停功能还可为 NDIS 提供查询驱动程序特征的机会，并重新配置堆栈的其他特征。

例如，NDIS 可以暂停驱动程序堆栈，以便在执行即插即用操作之前暂时停止数据流，如添加或删除筛选器驱动程序，或绑定或取消绑定协议驱动程序。 在进行重新配置后，NDIS 会重启堆栈。

微型端口和筛选器驱动程序通过函数接口处理暂停和重启服务。 协议驱动程序通过即插即用事件通知来处理暂停和重启服务。

有关暂停和重新启动操作的详细信息，请参阅 [驱动程序堆栈管理](driver-stack-management.md)。

 

 





