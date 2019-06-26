---
title: 框架 I/O 请求对象
description: 框架 I/O 请求对象
ms.assetid: e48437ee-597d-45b1-9093-8d5921356af5
keywords:
- UMDF 对象 WDK，I/O 请求对象
- framework 对象 WDK UMDF，I/O 请求对象
- I/O 请求对象 WDK UMDF
- IWDFIoRequest
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85fd159c2d0473d3de748df0eb0c9cd7395f84d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384470"
---
# <a name="framework-io-request-object"></a>框架 I/O 请求对象


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

向驱动程序通过公开 framework I/O 请求对象[IWDFIoRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)接口。 它封装 I/O 操作的详细信息。 所有 I/O 请求都表示为 framework I/O 请求对象。 该发送程序作为应用程序 I/O 操作，如 Microsoft Win32 调用的结果时该发送程序接收的 I/O 请求数据包 (IRP) 通知驱动程序主机进程[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)或**ReadFile**函数。 反射器通知，响应中的框架，构造一个新的请求对象，并将其放在相应的 I/O 队列中。 队列配置和选择的用户模式驱动程序的锁定模型确定当请求提供给该驱动程序。 有关详细信息，请参阅[I/O 队列配置调度模式](configuring-dispatch-mode-for-an-i-o-queue.md)并[指定回调同步模式](specifying-a-callback-synchronization-mode.md)。

 

 





