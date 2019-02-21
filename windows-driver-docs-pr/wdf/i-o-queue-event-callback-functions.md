---
title: I/O 队列事件的回调函数
description: I/O 队列事件的回调函数
ms.assetid: 5aa63c47-493d-4583-9eaa-1e50fdc089dd
keywords:
- I/O 队列 WDK UMDF
- 队列 WDK UMDF
- 回调函数 WDK UMDF
- 事件回调函数 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 652201844dbe6a7035125b3126f6454a144d4205
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524438"
---
# <a name="io-queue-event-callback-functions"></a>I/O 队列事件的回调函数


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当驱动程序创建的 I/O 队列，或配置默认的 I/O 队列时，他们可以注册以下接口，以便框架通知驱动程序，通过调用相关的接口的事件发生时与接口-相关联的方法。 有关 I/O 队列以及创建和配置的 I/O 队列的详细信息，请参阅[Framework I/O 队列对象](framework-i-o-queue-object.md)。

[IQueueCallbackCreate](https://msdn.microsoft.com/library/windows/hardware/ff556837)

[IQueueCallbackDeviceIoControl](https://msdn.microsoft.com/library/windows/hardware/ff556852)

[IQueueCallbackRead](https://msdn.microsoft.com/library/windows/hardware/ff556872)

[IQueueCallbackWrite](https://msdn.microsoft.com/library/windows/hardware/ff556882)

[IQueueCallbackDefaultIoHandler](https://msdn.microsoft.com/library/windows/hardware/ff556843)

 

 





