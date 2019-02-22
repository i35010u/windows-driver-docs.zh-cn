---
title: 增强的运行时重新配置功能
description: 增强的运行时重新配置功能
ms.assetid: 810d3acb-34ba-4b38-9410-dcdf76f1bb65
keywords:
- 驱动程序堆栈 WDK 连接网络、 暂停
- 驱动程序堆栈 WDK 连接网络、 重新启动
- 正在暂停驱动程序堆栈 WDK 网络
- 重新启动驱动程序堆栈 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a323b321c1b51bc490d35f379ae5381d8776cbd5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533453"
---
# <a name="enhanced-run-time-reconfiguration-abilities"></a>增强的运行时重新配置功能





NDIS 6.0 引入了暂停和重新启动而无需关闭堆栈并生成一个新的驱动程序堆栈的功能。 所有 NDIS 6.0 和更高版本的驱动程序必须支持暂停和重新启动服务。

通过将所有驱动程序放在已知状态，重新配置发生之前暂停堆栈消除了同步问题。 若要暂停的功能还使 NDIS 能够查询驱动程序的特征，并重新配置堆栈的其他特征。

NDIS 可以暂停驱动程序堆栈，例如，若要暂时停止数据流，然后才能执行插操作，例如添加或删除筛选器驱动程序，或绑定或取消绑定协议驱动程序。 NDIS 重新配置后，将重新启动堆栈。

微型端口和筛选器驱动程序处理暂停和重新启动服务通过函数的接口。 协议驱动程序处理暂停和重新启动服务通过插事件通知。

暂停和重启操作有关的详细信息，请参阅[驱动程序堆栈管理](driver-stack-management.md)。

 

 





