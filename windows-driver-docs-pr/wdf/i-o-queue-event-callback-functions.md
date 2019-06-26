---
title: I/O 队列事件回调函数
description: I/O 队列事件回调函数
ms.assetid: 5aa63c47-493d-4583-9eaa-1e50fdc089dd
keywords:
- I/O 队列 WDK UMDF
- 队列 WDK UMDF
- 回调函数 WDK UMDF
- 事件回调函数 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7ff812fb811f538e8f100dfc5fc9218f9e23a6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382833"
---
# <a name="io-queue-event-callback-functions"></a>I/O 队列事件回调函数


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当驱动程序创建的 I/O 队列，或配置默认的 I/O 队列时，他们可以注册以下接口，以便框架通知驱动程序，通过调用相关的接口的事件发生时与接口-相关联的方法。 有关 I/O 队列以及创建和配置的 I/O 队列的详细信息，请参阅[Framework I/O 队列对象](framework-i-o-queue-object.md)。

[IQueueCallbackCreate](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackcreate)

[IQueueCallbackDeviceIoControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)

[IQueueCallbackRead](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackread)

[IQueueCallbackWrite](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackwrite)

[IQueueCallbackDefaultIoHandler](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iqueuecallbackdefaultiohandler)

 

 





