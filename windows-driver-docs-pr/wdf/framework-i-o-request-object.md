---
title: 框架 I/O 请求对象
description: 框架 I/O 请求对象
ms.assetid: e48437ee-597d-45b1-9093-8d5921356af5
keywords:
- UMDF 对象 WDK，i/o 请求对象
- framework 对象 WDK UMDF，i/o 请求对象
- I/o 请求对象 WDK UMDF
- IWDFIoRequest
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 261c94bc078dca0f75e8d4dffa93bc6826e8572d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185541"
---
# <a name="framework-io-request-object"></a>框架 I/O 请求对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

框架 i/o 请求对象由 [IWDFIoRequest](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest) 接口向驱动程序公开。 它封装了 i/o 操作的详细信息。 所有 i/o 请求都表示为框架 i/o 请求对象。 当反射器接收到 i/o 请求数据包 (IRP) 作为应用程序 i/o 操作的结果（例如，调用 Microsoft Win32 [**CreateFile**](/windows/desktop/api/fileapi/nf-fileapi-createfilea) 或 **ReadFile** 函数）时，反射器通知驱动程序主机进程。 框架在响应反射器通知时，构造新的请求对象并将其放入相应的 i/o 队列。 队列配置和用户模式驱动程序选择的锁定模型确定何时向驱动程序提供请求。 有关详细信息，请参阅为 [I/o 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md) 和 [指定回调同步模式](specifying-a-callback-synchronization-mode.md)。

 

