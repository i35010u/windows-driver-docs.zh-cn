---
title: 移植 I/O 队列
description: 移植 I/O 队列
ms.assetid: 90319342-5FAB-451B-BCA1-B273B81418DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18fe656759e9492fbe1a2875048e7ccf5ddeb40e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390094"
---
# <a name="porting-io-queues"></a>移植 I/O 队列


WDF 驱动程序创建队列并注册中的 I/O 事件回调[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)回调。 默认情况下，每个 I/O 队列对象是一个设备对象的子级。 WDF 驱动程序可以配置为每个队列的以下任务：

-   I/O 请求类型将定向到队列。
-   是否请求调度并行 （只要到达时），按顺序 （一次一个），或手动 （根据驱动程序请求）。
-   是否同时或按顺序称为 I/O 事件回调例程。
-   是否在 framework 或驱动程序管理系统和设备电源转换通过队列。

有关创建队列的详细信息，请参阅[创建 I/O 队列](creating-i-o-queues.md)

 

 





