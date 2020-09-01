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
ms.openlocfilehash: d19e70b6802436de6e12a49fb3ffcc25fe477d3f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191209"
---
# <a name="io-queue-event-callback-functions"></a>I/O 队列事件回调函数


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

当驱动程序创建 i/o 队列，或配置默认 i/o 队列时，它们可以注册下面的接口，以便通过调用与接口关联的方法（在出现与接口相关的事件时），使框架通知驱动程序。 有关 i/o 队列以及创建和配置 i/o 队列的详细信息，请参阅 [框架 I/o 队列对象](framework-i-o-queue-object.md)。

[IQueueCallbackCreate](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackcreate)

[IQueueCallbackDeviceIoControl](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdeviceiocontrol)

[IQueueCallbackRead](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackread)

[IQueueCallbackWrite](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackwrite)

[IQueueCallbackDefaultIoHandler](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iqueuecallbackdefaultiohandler)

 

