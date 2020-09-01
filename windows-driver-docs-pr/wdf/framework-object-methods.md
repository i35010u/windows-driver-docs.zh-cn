---
title: 框架对象方法
description: 框架对象方法
ms.assetid: f82275c5-15f9-43f5-91bb-b83446526c28
keywords:
- framework 对象 WDK KMDF，方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d0d6480ca37b02d673f8508c9a2fc211e217644
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188709"
---
# <a name="framework-object-methods"></a>框架对象方法





每个框架对象)  (函数导出一组方法。 每个方法都有两种用途：

-   它执行与对象关联的操作。

    例如， [**WdfIoQueueCreate**](/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate) 方法为设备创建 i/o 队列。

    执行操作的方法通常会返回一个 [NTSTATUS 值](https://docs.microsoft.com/windows-hardware/drivers/kernel/ntstatus-values)。

-   它检索或修改与对象相关联的 [属性](framework-object-properties.md) 。

    例如， [**WdfRequestGetInformation**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetinformation) 方法返回有关 i/o 请求完成状态的信息。

    检索属性的方法通常会返回属性的值，而修改属性的方法通常不会返回值。

每个对象方法都接受对象句柄作为输入。 如果驱动程序向对象方法传递的对象句柄无效，则会发生系统 bug 检查。

 

