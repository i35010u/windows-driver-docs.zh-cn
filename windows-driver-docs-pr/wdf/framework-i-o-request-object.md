---
title: 框架 I/O 请求对象
description: 框架 I/O 请求对象
keywords:
- UMDF 对象 WDK，i/o 请求对象
- framework 对象 WDK UMDF，i/o 请求对象
- I/o 请求对象 WDK UMDF
- IWDFIoRequest
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc96965f70aad70c7ea4fc87fb300e042cae7c15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815701"
---
# <a name="framework-io-request-object"></a>框架 I/O 请求对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架 i/o 请求对象由 [IWDFIoRequest](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest) 接口向驱动程序公开。 它封装了 i/o 操作的详细信息。 所有 i/o 请求都表示为框架 i/o 请求对象。 当反射器接收到 i/o 请求数据包 (IRP) 作为应用程序 i/o 操作的结果（例如，调用 Microsoft Win32 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 或 **ReadFile** 函数）时，反射器通知驱动程序主机进程。 框架在响应反射器通知时，构造新的请求对象并将其放入相应的 i/o 队列。 队列配置和用户模式驱动程序选择的锁定模型确定何时向驱动程序提供请求。 有关详细信息，请参阅为 [I/o 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md) 和 [指定回调同步模式](specifying-a-callback-synchronization-mode.md)。

 

