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
ms.openlocfilehash: 3428603723fa64873aa2a80f1f2e91aa58859dbb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843171"
---
# <a name="framework-io-request-object"></a>框架 I/O 请求对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

框架 i/o 请求对象由[IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)接口向驱动程序公开。 它封装了 i/o 操作的详细信息。 所有 i/o 请求都表示为框架 i/o 请求对象。 当反射器接收到 i/o 请求数据包（IRP）作为应用程序 i/o 操作（例如，调用 Microsoft Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)或**ReadFile**函数）的结果时，反射器通知驱动程序主机进程。 框架在响应反射器通知时，构造新的请求对象并将其放入相应的 i/o 队列。 队列配置和用户模式驱动程序选择的锁定模型确定何时向驱动程序提供请求。 有关详细信息，请参阅为[I/o 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)和[指定回调同步模式](specifying-a-callback-synchronization-mode.md)。

 

 





