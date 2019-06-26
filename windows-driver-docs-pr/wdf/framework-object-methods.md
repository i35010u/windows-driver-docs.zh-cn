---
title: 框架对象方法
description: 框架对象方法
ms.assetid: f82275c5-15f9-43f5-91bb-b83446526c28
keywords:
- framework 对象 WDK KMDF，方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dd19a2818854f2bd820c59e480463d651881283
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384460"
---
# <a name="framework-object-methods"></a>框架对象方法





每个框架对象将导出一的组方法 （函数）。 每个方法有两个目的之一：

-   它执行与对象相关联的操作。

    例如， [ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)方法创建设备的 I/O 队列。

    通常执行的操作的方法将返回[NTSTATUS 值](https://docs.microsoft.com/windows-hardware/drivers/kernel/ntstatus-values)。

-   它检索或修改[属性](framework-object-properties.md)与对象相关联。

    例如， [ **WdfRequestGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)方法返回的 I/O 请求的完成状态有关的信息。

    检索一个属性通常的方法返回属性的值，而通常修改属性的方法不返回值。

每个对象方法接受对象句柄作为输入。 如果驱动程序将无效的对象句柄传递给对象方法，检查系统错误发生。

 

 





