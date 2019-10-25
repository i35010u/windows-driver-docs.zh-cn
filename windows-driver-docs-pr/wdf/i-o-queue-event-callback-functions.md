---
title: I/O 队列事件回调函数
description: I/O 队列事件回调函数
ms.assetid: 5aa63c47-493d-4583-9eaa-1e50fdc089dd
keywords:
- I/o 队列 WDK UMDF
- 队列 WDK UMDF
- 回调函数 WDK UMDF
- 事件回调函数 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f98e089e7fb91826bd3d85406b57d7acf9b5c527
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845216"
---
# <a name="io-queue-event-callback-functions"></a>I/O 队列事件回调函数


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当驱动程序创建 i/o 队列，或配置默认 i/o 队列时，它们可以注册下面的接口，以便通过调用与接口关联的方法（在出现与接口相关的事件时），使框架通知驱动程序。 有关 i/o 队列以及创建和配置 i/o 队列的详细信息，请参阅[框架 I/o 队列对象](framework-i-o-queue-object.md)。

[IQueueCallbackCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackcreate)

[IQueueCallbackDeviceIoControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)

[IQueueCallbackRead](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackread)

[IQueueCallbackWrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackwrite)

[IQueueCallbackDefaultIoHandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdefaultiohandler)

 

 





