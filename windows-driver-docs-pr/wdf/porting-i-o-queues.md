---
title: 移植 I/O 队列
description: 移植 I/O 队列
ms.assetid: 90319342-5FAB-451B-BCA1-B273B81418DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01923c4f80e55c3adbeb07ac40c0dd0cf7e5c8cf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842254"
---
# <a name="porting-io-queues"></a>移植 I/O 队列


WDF 驱动程序在[*EvtDriverDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调中创建队列并注册 i/o 事件回调。 默认情况下，每个 i/o 队列对象都是设备对象的子对象。 WDF 驱动程序可以为每个队列配置以下任务：

-   哪些 i/o 请求类型将定向到队列。
-   请求是按顺序（一次一个地）、按顺序（一次）或手动方式（在驱动程序请求时）按顺序调度请求。
-   I/o 事件回调例程是并行调用还是按顺序调用。
-   框架或驱动程序是否通过系统和设备电源转换管理队列。

有关创建队列的详细信息，请参阅[创建 I/o 队列](creating-i-o-queues.md)

 

 





