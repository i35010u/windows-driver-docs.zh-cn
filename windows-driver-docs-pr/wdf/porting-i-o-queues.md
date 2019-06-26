---
title: 移植 I/O 队列
description: 移植 I/O 队列
ms.assetid: 90319342-5FAB-451B-BCA1-B273B81418DB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c050bb2e22959ccc263884802d1b45c6d1a0129
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379635"
---
# <a name="porting-io-queues"></a>移植 I/O 队列


WDF 驱动程序创建队列并注册中的 I/O 事件回调[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调。 默认情况下，每个 I/O 队列对象是一个设备对象的子级。 WDF 驱动程序可以配置为每个队列的以下任务：

-   I/O 请求类型将定向到队列。
-   是否请求调度并行 （只要到达时），按顺序 （一次一个），或手动 （根据驱动程序请求）。
-   是否同时或按顺序称为 I/O 事件回调例程。
-   是否在 framework 或驱动程序管理系统和设备电源转换通过队列。

有关创建队列的详细信息，请参阅[创建 I/O 队列](creating-i-o-queues.md)

 

 





