---
title: Framework 对象方法
description: Framework 对象方法
ms.assetid: f82275c5-15f9-43f5-91bb-b83446526c28
keywords:
- framework 对象 WDK KMDF，方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9954c646788651ed1045fa64c60193adf82c53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547014"
---
# <a name="framework-object-methods"></a>Framework 对象方法





每个框架对象将导出一的组方法 （函数）。 每个方法有两个目的之一：

-   它执行与对象相关联的操作。

    例如， [ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)方法创建设备的 I/O 队列。

    通常执行的操作的方法将返回[NTSTATUS 值](https://msdn.microsoft.com/library/windows/hardware/ff557697)。

-   它检索或修改[属性](framework-object-properties.md)与对象相关联。

    例如， [ **WdfRequestGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549965)方法返回的 I/O 请求的完成状态有关的信息。

    检索一个属性通常的方法返回属性的值，而通常修改属性的方法不返回值。

每个对象方法接受对象句柄作为输入。 如果驱动程序将无效的对象句柄传递给对象方法，检查系统错误发生。

 

 





